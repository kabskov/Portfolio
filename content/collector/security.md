---
title: "Keeping users out of each other's finds"
weight: 1
series: ["The Collector"]
series_order: 4
---
 
Users log in with their email and password and get a token (a JWT) that is valid for one hour. The client sends the token with every request to show who it is. Passwords are hashed with BCrypt, which means they are scrambled in a way that cannot be turned back, and they are never returned in a response.
 
Every route has a role, and two handlers, one for authentication (who are you?) and one for authorization (are you allowed?), run before each route to check the token and the role.
 
But a valid token is not enough. A user should not be able to change the number in the URL and read someone else's finds. That is what `requireOwner` is for: it compares the `userId` in the URL with the one in the token.
 
Two small decisions I am happy with:
 
- **The user id comes from the token when a find is registered, never from the request body.** That way a user cannot register a find on another user's account by sending a different id.
- **A find that belongs to someone else returns 404, not 403.** If the API said 403 for other people's finds and 404 for finds that do not exist, anyone could try ids one by one and learn which ones exist, for example how many finds the app has. With 404 in both cases, the two answers look the same.