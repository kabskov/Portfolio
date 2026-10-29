---
title: "From user stories to test cases"
weight: 1
---
 
The Collector has eleven user stories, all written from the point of view of a rock collector. My first draft had several reasons and solutions in each story, separated by slashes. Now every story has one reason, and the extra ideas (map, statistics, filtering) are on a list of future ideas.
 
Each story also has acceptance criteria in Given/When/Then form, for example: *Given I am logged in, when I fetch another user's finds, then I get 403.*
 
The criteria make it easy to see what still needs to be implemented. Story 11 (image upload) is only partly done, since the API stores a photo URL but cannot upload a file. I have marked it that way in the README instead of hiding it.
 
The criteria are also a ready-made list of test cases for my Rest Assured tests.