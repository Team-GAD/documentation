---
layout: default
title: Backend
parent: Gateway
nav_order: 1
---

## Gateway Backend

The gateway backend has several tasks. 
First, it communicates with the Cups via the MQTT broker. 
It also writes all relevant data to the MongoDb.

In addition, the gateway communicates with the cloud, it 
loads user data from the cloud and pushes this data back into the 
cloud at the end of an event.  

Finally, the backend also provides many API endpoints for the frontend.

The following endpoints are provided:

- `GET /`
Returns "Welcome to the Gateway backend!"
- `GET /cup/scan`
Performs a nfc scan and returns either a cupid or an error
- `GET /cup/ping/{id}`
Flashes the LED of the corresponding cup for a short time
- `GET /cup/{id}`
Returns a Cup {	Id string, Bat int, UserHandle string}
- `POST /cup/{id}/mode`
Sets the cup in the corresponding mode
- `GET /cups`
Returns all cups
- `GET /game/{id}`
Returns the current game
- `GET /next`
Used for the GuessWho game to get a new guess
- `GET /winner`
Used for the GuessWho game to get the winner
- `GET /user/{cupId}/disconnect`
Disconnects a user form a cup and uploads the data to the cloud
- `POST /user/order`
Performs a scan and then adds a drink to the scanned user
- `GET /user/{userHandle}/check`
Downloads user information from the cloud 
- `GET /user/{userHandle}/cup/{cupId}/connect`
Performs a scan and connects the user with the scanned cup
- `GET /leaderboard`
Returns the leaderboard of all games 

For Demo purposes:

- `GET /off`
Shuts down the LED for all cups
- `GET /charge`
Sets all cups into the charging LED mode
