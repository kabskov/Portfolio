---
title: "Choosing an external API"
weight: 1
series: ["The Collector"]
series_order: 3
---
 
I wanted an API that is actually useful for my project, not one I picked just because I had to have one. The Collector lets users register where they found a stone, so a service that turns a place name into coordinates (geocoding) was the natural choice.
 
### Why Nominatim
I looked at mineral databases like Mindat, but they are made for cataloguing mineral species, not for everyday finds like sea glass or skipping stones on a Danish beach. It would be great to look up what stone you just found and learn more about it, but that does not match my needs for version 1.
 
What I need is a place lookup. Nominatim (OpenStreetMap's geocoding service) is free, needs no API key, and knows the small local places a Danish collector would type in.
 
### Following its rules
Nominatim is free, so it has a few strict rules:
 
- No more than **one request per second**.
- Every request must say which app it comes from, using a **User-Agent** header.
- No autocomplete, which means no searching on every keystroke.

In `FindSpotService` I send a User-Agent and wait one second before each call. The lookup only runs when a find is registered with a find spot keyword.
 
### Shaping the service around the response 
- `/search` returns a list of places, sorted by how well they match. I only use the **first result**. This is a design choice to keep version 1 simple. Letting the user choose from a list would need a frontend with an extra step, and more endpoints. The downside is that a place name that exists several times could give the wrong place. In a later version I could return the whole list and let the user pick.
- If the list is empty, the API returns 404.
- The coordinates come back as strings. My `FindSpotDTO` has `double` fields mapped with `@JsonProperty("lat")` and `("lon")`, and Jackson converts them for me.
- I store the full `display_name` (for example "Roskilde, Roskilde Kommune, Region Sjælland, Denmark") together with the coordinates, because it says more next to a find than two decimal numbers.
- If Nominatim cannot be reached, the API returns 502, and the error is logged.

I do not store the detailed address breakdown in version 1, since the scope does not need it.
 
### What's left
`FindSpotService` is only tested indirectly, through the find service test. It should have its own tests.