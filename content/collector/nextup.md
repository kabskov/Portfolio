---
title: "What I'd do next"
weight: 1
---
 
The Collector works, but I am clear about what it cannot do yet.
 
### Known limitations
- **No image upload.** I wanted it in version 1, but did not get to it. The API stores a photo URL, but you cannot upload a file.
- **Find ids are global.** All users' finds are in one table, so one user's finds can have ids like 1, 2 and 5, and another user's 3, 4 and 6. The user sees the id, which is confusing. I could show a running number for each user instead, or hide the id.
- **No filtering or sorting in the API.** My DAO can already find finds by date, category and find spot, but those queries are not connected to any endpoints.
- **Weak validation.** I check that fields are present, but not that a password is long enough or that an email looks like an email.
- **The find spot cannot be changed** after a find has been created.

### Ideas for later
A map of the finds, statistics on where I find the most, a reference guide to the stones, and favorites.