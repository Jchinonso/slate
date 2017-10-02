---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:

  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

PostIt is a simple application that allows friends and colleagues create groups for notifications. This way one person can post notifications to everyone by sending a message once. The application allows people create accounts, create groups and add registered users to the groups, and then send messages out to these groups whenever they want.

# Development


The application was developed with [NodeJs](http://nodejs.org) and [Express](http://expressjs.com) is used for routing. The [Postgres](http://postgresql.com) database was used with [sequelize](http://sequelizejs.com) as the ORM


#Installation

1.  Ensure you have NodeJs and postgres installed
2.  Clone the repository `https://github.com/jchinonso/PostIt`
3.  Change your directory `cd PostIt`
4.  Install all dependencies `npm install`
5.  Start the app `npm run start:dev` for development Or
6.  Run `npm start` to use transpiled code
7.  Use [postman](https://www.getpostman.com/) to consume the API

# Authentication

PostIt uses (email and password) to login to allow access to the API protected routes. On registering or login, a token is generated.
postIt expects for the token to be included in all API requests to the server in a header that looks like the following:
x-access-token: token

# Api Summary

## Below are the API endpoints and their functions
EndPoint                        |   Functionality
--------------------------------|------------------------
POST /api/user/signin           |   Logs a user in.
POST /api/user/signup           |   Create a new user.            
GET /api/user                   |   Get all users.
POST /api/group                 |   Creates a new group.
POST /api/group/groupid/user    |   Add user to group.
POST /api/group/groupid/message |   Add message to group.
GET /api/group/groupid/message  |   Get all messages that belongs to group.


# Users

## Sign up User
### Request

  * Endpoint: Post: `/api/v1/user/signup` 
  * Body  `(application/json)` 

### Response
  * Status: `201 created` 
  * Body  `(application/json)` 


> Request:

```json
 {
    "username": "jchinonso12",
    "email": "johnsonchinonso919@gmail.com",
    "password": "password",
    "phoneNumber": "08139308818",
  },

```
<aside class="notice">You must set the token at the header after sign up to access protected routes (x-access-token: token)</aside>

> Response:

```json
 {
   "id": 1,
    "username": "jchinonso12",
    "email": "johnsonchinonso919@gmail.com",
    "phoneNumber": "08139308818",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImpjaGlub25zbzEyIiwidXNlcklkIjozLCJlbWFpbCI6ImpvaG5zb25jaGlub25zbzkxOUBnbWFpbC5jb20iLCJpYXQiOjE1MDU5MDY0NDgsImV4cCI6MTUwNjA3OTI0OH0.ZAQBAUM9EJ1JP60VqmcfvmbBawOIqpZwphLLzrruCyg"
}

```

## Sign in User
### Request

  * Endpoint: Post: `/api/v1/user/signin` 
  * Body  `(application/json)` 

### Response
  * Status: `200 created` 
  * Body  `(application/json)` 

<aside class="notice">You must set the token at the header after login to access protected routes (x-access-token: token)</aside>

> Request:

```json
 {
    "email": "johnsonchinonso919@gmail.com",
    "password": "password",
 },

```

> Response:

```json
{
    "msg": "You have been loggedin successfully",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImpjaGlub25zb29vIiwidXNlcklkIjoxLCJlbWFpbCI6ImpvaG51dUBnbWFpbC5jb20iLCJpYXQiOjE1MDU4MDE1ODksImV4cCI6MTUwNTk3NDM4OX0.DiDVLiuM75wwnbw8XMS0bNMBBnkh0WG9RBqqA4i7LuQ"
}

```

# Groups
## Create Group

### Request

  * Endpoint: Post: `/api/v1/group` 
  * Body  `(application/json)` 

### Response
  * Status: `201 created` 
  * Body  `(application/json)` 

> Request:

```json
 {
    "name": "Nairobi-fellows",
    "description": "Talks about andela kenya"
  },

```
<aside class="notice">You must set the token at the header after sign up to access protected routes (x-access-token: token)</aside>

> Response:

```json
 {
    "id": 1,
    "name": "Nairobi-fellows",
    "description": "Talks about andela kenya",
    "creator": "jchinonsooo"
}

```

## Retrieve all Groups

### Request

  * Endpoint: Get: `/api/v1/group` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 


> Response:

```json
 {
    "groups": [
        {
            "id": 1,
            "name": "Nairobi-fellows",
            "description": "talks about andela nairobi",
            "creator": "jdoe",
            "createdAt": "2017-09-20T19:56:54.681Z"
        }
    ]
}
```

## Add User to Group

### Request

  * Endpoint: Post: `/api/v1/group/groupId/user` 
  * Body  `(application/json)` 

### Response
  * Status: `201 created` 
  * Body  `(application/json)` 

> Request:

```json
 {
    "username": "johnnyp",
  },

```

> Response:

```json
{
  "msg": "User added successfully to Group"
}

```
## Retrieve all Group Members

### Request

  * Endpoint: Get: `/api/v1/group/groupId` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 


> Response:

```json
 {
    "groupMembers": [
        {
            "id": 1,
            "username": "jdoe",
            "email": "johnuu@gmail.com",
            "phoneNumber": "997897898797879",
            "createdAt": "2017-09-20T19:55:51.699Z"
        },
        {
            "id": 2,
            "username": "johnny",
            "email": "johnnyp@gmail.com",
            "phoneNumber": "997897898797879",
            "createdAt": "2017-09-20T19:56:22.891Z"
        },
    ]
}
```

## Add Message to Group

### Request

  * Endpoint: Post: `/api/v1/group/groupId/message` 
  * Body  `(application/json)` 

### Response
  * Status: `201 created` 
  * Body  `(application/json)` 

> Request:

```json
 {
    "content": "i need some pizza",
    "priority": "mormal"
  },

```

> Response:

```json
{
    "id": 1,
    "content": "i need some pizza",
    "sender": "jdoe",
    "priority": "normal",
    "isRead": false,
    "createdAt": "2017-09-20T20:43:01.042Z"
}

```

## Retrive all Group Messages 

### Request

  * Endpoint: Get: `/api/v1/group/groupId/message` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 


> Response:

```json
{
    "messages": [
        {
            "id": 1,
            "content": "i love pizza",
            "priority": "normal",
            "groupId": 1,
            "sender": "jdoe",
            "isRead": false,
            "createdAt": "2017-09-20T20:43:01.042Z",
            "updatedAt": "2017-09-20T20:43:01.042Z"
        }
    ]
}

```


