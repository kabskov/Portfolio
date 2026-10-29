---
title: "The Collector"
weight: 1
series: ["The Collector"]
series_order: 1
---

*A web application for rock collectors to register their finds — including find spots, photos and notes — built as a 
third-semester portfolio project for my AP degree in Computer Science.*

### The idea
I love hunting for hagstones — and I love actually finding one even more!
When I do find one, I usually take a photo of it to somehow document my find. The problem with those photos is 
that they quickly disappear among photos of my cat and screenshots of things I don't want to forget.
That's how the idea for this application came about: a place where I can save photos, notes, and find 
spots for my hagstones (and other beautiful or interesting stones).

### The scope
I will try to keep the application fairly simple, so I can better focus on the individual features — quality over quantity.
Version 1 will therefore have the following scope limitations:

- The application is for personal use. This means a user's registered finds are not shared with other users. 
- You must create a user account and be logged in to use the application. 
- You can register a find spot by typing in a location — not by having the application retrieve your location or by tapping on a map. 
- Categories are limited to: hagstones, fossils, pretty stones, flint stones, skipping stones, sea glass, quartz, other. 
- The application is built as a web application for use in a browser. 
- The user can view a list of all their finds, but cannot filter them.

### The vision
In the longer term, the application should be able to show a map of one's stone finds and make it possible to discover 
patterns in where one has made the most finds.
The application should also include a reference guide with information about the stones that can be 
selected as categories — including which stones one can expect to find in different countries and landscapes, 
as well as how natural history has shaped these finds, for example how the ice age has shaped the landscape and 
the stones one can find in it today.
Finally, it should be possible to mark stone finds as favorites, so they are collected in a separate list.

### Getting there
That's the long-term vision. But before I get there, I need a solid foundation to build on — and that's exactly what this semester's project setup is designed to give me.

### What's the setup for the project?

Our third semester project mirrors how software is built in practice: incrementally, with new requirements, new technologies, and continuous reflection.

**The Core Idea**

We will:
- Choose our own application idea
- Build it incrementally over the semester
- Extend the application with new technologies and reflect on our progress each week

**Timeline for the backend**

Weeks 1-10: The goal after week 10 is a production-ready backend API. During these weeks, we'll gradually add:

- Java + Maven project structure
- REST API and endpoints
- JPA / database persistence
- External API integration
- Validation and error handling
- Integration tests
- JWT-based authentication and authorization
- Configuration and environment variables
- Deployment

This project is designed to help us answer a very real question: 
> Can I actually build and evolve a backend system?