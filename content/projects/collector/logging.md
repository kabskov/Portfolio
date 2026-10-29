---
title: "Errors and logging"
weight: 70
series: ["The Collector"]
series_order: 7
---
 
When something goes wrong "on purpose", for example a wrong password or a find that does not exist, the code throws an `ApiException` with a status code and a message. These are errors I expect, as opposed to bugs.
 
One handler in `ApplicationConfig` catches every `ApiException` and turns it into the same JSON format everywhere:
 
```json
{ "status": 404, "msg": "..." }
```
 
The same exception class also does the logging. Client errors (4xx), where the user did something wrong, are logged as warnings. Server errors (5xx), where something is wrong on my side, are logged as errors with the stack trace. That way the log shows what needs attention. A wrong password is not an emergency, but an `ERROR` could mean that the database is not responding, that Nominatim cannot be reached, or that there is a bug I did not expect.
 
Passwords and tokens are never logged. I log ids instead, for example when a user or a find is created.