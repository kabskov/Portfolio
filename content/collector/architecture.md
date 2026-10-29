---
title: "Layers, DTOs and mappers"
weight: 1
series: ["The Collector"]
series_order: 9
---
 
The Collector is split into three layers, and each one has one job:
 
- **Controllers** read the request from the client and write the response. They contain no business logic.
- **Services** validate input and decide what should happen.
- **DAOs** talk to the database. They all implement the same generic `IDAO` interface.

Between the layers, **DTOs** carry the data, and **mappers** convert between entities and DTOs. A request travels from the controller to the service to the DAO, and the answer travels back the same way.

### Why DTOs?
The API never sends entities out. A DTO is a small class that holds exactly the data the client should see or send. That has three advantages:
 
- I decide what leaves the API. An entity can contain things the client should never see, like a password hash.
- The API stays the same, even if I change the database tables later.
- It avoids an endless loop. A User has a set of finds, and every Find points back to its User. If I turned an entity into JSON directly, it would go from user to finds to user to finds, and never stop.

Examples: 
- `UserDTO` has `password` as write-only, so it can be sent in but never comes back out.
- `role` is read-only, so a user cannot choose to be an admin.
- `FindDTO` has a list of `categoryIds` instead of full category objects, and the `userId` instead of the whole user.

### Mappers 
My mappers are small classes with static methods, for example `FindMapper.convertToFindDTO(find)`. A static method can be called without creating an object first. The mappers do not need to remember anything - they just take an input and return an output, so there is no reason to create a mapper object. All the conversion is in one place, and the services stay easy to read.
 
### Where I put the validation
The validation lives in the service layer, for example "A find must have at least one category". The DAOs only handle the database, and the controllers do not know any rules. That makes it clear where to look when something goes wrong.