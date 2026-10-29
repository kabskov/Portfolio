---
title: "Documenting the API"
weight: 100
series: ["The Collector"]
series_order: 10
---
 
My API is documented with a table of all endpoints (method, URL, role, request, response and possible errors), followed by the JSON formats and a list of error codes. I followed the course guide, but added a column for the role, since my routes are protected.
 
For each endpoint I look at the DTOs, the service and the controller, and answer the same questions: what does the client send, what comes back, and what can go wrong?
 
That turned out to be a good way to review my own code. Along the way I found things I had not thought about:
 
- Which endpoints check that you are the owner, and whether `registerFind` uses the id from the token. It does, so no one can register a find on someone else's account.
- What a user gets if the id in the URL is not a number. Without a handler for that, it would be a 500 instead of a 400.
- Small details that clients need to know, like that PATCH only changes the fields you send, and that the find spot can only be set when a find is created.

All errors have the same format, `{ "status": 404, "msg": "..." }`, and each status code has a short list of messages and when they happen.