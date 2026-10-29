---
title: "Testing the API"
weight: 60
series: ["The Collector"]
series_order: 6
---
 
I test at two levels:
 
**DAO and service tests** run against a real Postgres database. Testcontainers starts it in a Docker container, just for the tests, so I am not testing against a fake. Before each test, a small populator empties the tables and inserts fresh users, categories and finds. That way the tests do not depend on hard-coded ids.
 
**Rest Assured tests** start the real Javalin server, send HTTP requests to the endpoints and check the status code and the JSON. They follow the acceptance criteria from my user stories, so every Given/When/Then becomes a test.
 
One of the tests found a real bug. The date of a find came back as `[2026, 6, 20]` instead of `"2026-06-20"`, which is not what my documentation says. Jackson writes dates as numbers unless you tell it not to. I fixed it by changing the JSON settings in `ApplicationConfig`.
 
Tests that call Nominatim are marked with a tag and left out of the Maven build. GitHub Actions runs the tests when I push, and if a test fails, no new version is built and deployed. I do not want a Nominatim outage to stop that.