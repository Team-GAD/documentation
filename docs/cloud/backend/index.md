---
layout: default
title: Backend
parent: Cloud
nav_order: 1
---

## Cloud Backend

The backend of the cloud service provides several functions in Node js which are deployed on a firebase server allowing any user and any event organizer to access and upload data at any time using a browser.
![functions](../../assets/images/functions.png)
The user authentication was tracked and secured with the Firebase Authentication functionality. The database and the triggers were handled using Cloud Firestore and the images were saved in the Firebase Storage.
By subscribing to the Firebase Blaze plan (https://firebase.google.com/pricing) it is possible to have several thousands of requests issued everyday and to integrate modules which need a lot of computational resources such as the face detection. 

We can split the functions in three categories:
I- Gateway API endpoints: 
  1- Sessions
    - `POST /event/:eventId/open`
      Creating or pulling a session for a user using the username and the eventId. The session consists of all the information The function is called when a user asks for a cup
    - `POST /event/:eventId/update`
      Updating the cheers, orders, score, alcohol percentage, bill and calories of a user. This function is used by the bartender to update the user information while the cup is still used.
    - `POST /event/:eventId/close`
      Closing the session and updating it
    - `GET /event/:eventId/user/:userHandle`
      The gateway can request informations about the user for identity confirmation
  2- Games
    - `POST /event/:eventId/game/players`


II- User API endpoints: 
  1- Authentication
    - `POST /signup`

    - `POST /login`
    
  2- Users
    - `GET /user`

    - `GET /users`
    
    - `GET /user/:handle`

    - `POST /user`

    - `POST /user/image`

  3- Events
- `GET /event/:eventId`

- `GET /event/:eventId/like`

- `GET /event/:eventId/unlike`

- `GET /session/:sessionId`

- `POST /game/blur`
  
  
III- Cloud Firestore triggers: 
- `onEventImageChange`

- `onUserImageChange`
