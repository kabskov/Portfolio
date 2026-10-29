---
title: "Building the domain"
weight: 20
series: ["The Collector"]
series_order: 2
---

The Collector has four entities: User, Find, Category and FindSpot. It looks simple on paper, but a few decisions turned out to be more interesting than I expected.
 
### Relations
- **User ↔ Find:** The two classes know about each other (a bidirectional relation). A find has a `user`, and a user has a set of `finds`. I want deleting a user to delete their finds too, and for that the User side has to know its finds. The `finds` collection is marked with `mappedBy`, which tells JPA that the `user` field in Find is the one that is stored in the database.
- **Find → Category:** A find can have several categories, and a category can belong to many finds (many-to-many). Only Find knows about this, so the relation goes one way.
- **Find → FindSpot:** Many finds can point to the same find spot (many-to-one). Only Find knows about it, and a find does not need a find spot.

### Cascade
Cascade means that something you do to one entity is passed on to the entities it is related to. I follow the course's advice to be conservative, so each relation only gets what I actually use:
 
- **User → Find: REMOVE.** Deleting a user deletes their finds.
- **Find → FindSpot: PERSIST.** Saving a find also saves its find spot.
- **Find → Category: nothing.** The categories already exist, so a find should never create or delete them.

 
### Why FindSpot has no setters
Several finds can point to the same FindSpot, for example "Roskilde". If FindSpot had a `setLatitude()` method, a line meant to fix the coordinates for one find would silently move every other find that uses the same spot.
 
I first tried to make the coordinates `final`, so they could not change. That does not work with JPA, which needs a constructor without arguments, and such a constructor cannot give a `final` field its value. So FindSpot simply has no setters. The values can be read, but not changed.
 
### JPQL
JPQL is the query language JPA uses. All my queries start from Find, because a find is what I want back, and follow the fields in Find. For example:
 
```sql
SELECT f FROM Find f JOIN f.categories c WHERE c.id = :categoryId
```
 
This means "give me all finds that have this category". It works without Category knowing anything about its finds, because the relation is defined in Find. None of my queries start from a user or a category and look for finds, so a one-way relation is enough.