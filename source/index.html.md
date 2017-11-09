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

Worklist is a simple todo list application that allows users to create lists of tasks to be completed and track their progress on these tasks.

# Development


The application was developed with [NodeJs](http://nodejs.org) and [Express](http://expressjs.com) is used for routing. The [MongoDb](https://www.mongodb.com/) database was used with [mongoose](https://mongoosejs.com) as the ODM


#Installation

1.  Ensure you have NodeJs and Mongodb installed
2.  Clone the repository `https://github.com/jchinonso/WorkList`
3.  Change your directory `cd WorkList`
4.  Install all dependencies `npm install`
5.  Start the app `npm start` for development Or
7.  Use [postman] to consume the API

# Authentication

CheckList uses (email and password) to login to allow access to the API protected routes. On registering or login, a token is generated.
CheckList expect the token to be included in the header as `x-access-token: token`. All API requests to the server are stated below


# Api Summary

## Below are the API endpoints and their functions
EndPoint                               |   Functionality
---------------------------------------|------------------------
POST /api/v1/user/signin               |   Logs a user in.
POST /api/v1/user/signup               |   Create a new user.            
GET /api/v1/user                       |   Get all users.
POST /api/v1/todo                      |   Creates a new todo.
POST /api/v1/todo/:todoId/task         |   Add task to todo.
POST /api/v1/todo/:todoId/collaborator |   Add collaborators to todo.
PUT /api/v1/todo/task/:taskId          |   Update a task.


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
    "name": "johnson chinonso",
    "username": "jchinonso12",
    "email": "johnsonchinonso919@gmail.com",
    "password": "password"
  },

```
<aside class="notice">You must set the token at the header after sign up to access protected routes (x-access-token: token)</aside>

> Response:

```json
 {
    "success": true,
    "name": "johnson chinonso",
    "username": "jchinonso12",
    "email": "johnsonchinonso919@gmail.com",
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
    "success": true,
    "message": "Successfully login!",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImpvaG5ueXAiLCJ1c2VySWQiOiI1YTAwMmM1MjRhN2JmY2MyYTc5MDg1NTEiLCJlbWFpbCI6ImpvaG5wQGdtYWlsLmNvbSIsImlhdCI6MTUwOTk2MDk0MywiZXhwIjoxNTEwMDQ3MzQzfQ.u6A5ASWlHgoiwPGQE-mUcgsgBdpGTc_BrXeXRqBCCaA"
}

```

# Todos
## Create Todo

### Request

  * Endpoint: Post: `/api/v1/todo` 
  * Body  `(application/json)` 

### Response
  * Status: `201 created` 
  * Body  `(application/json)` 

> Request:

```json
 {
    "text": "Studying"
 },

```
<aside class="notice">You must set the token at the header after sign up to access protected routes (x-access-token: token)</aside>

> Response:

```json
{
    "success": true,
    "todo": {
        "_id": "59fffb068ae3e0b2cd070d1f",
        "text": "Studying",
        "creator": {
            "_id": "59fc257d46900b201d9c1315",
            "username": "johnnyparagon",
            "name": "johnson chinonso"
        },
        "__v": 1,
        "tasks": [
            "59fffb278ae3e0b2cd070d20"
        ],
        "collaborators": [
            "59fc257d46900b201d9c1315"
        ]
    }
}

```

## Retrieve all Todos

### Request

  * Endpoint: Get: `/api/v1/todo` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 


> Response:

```json
{
    "success": true,
    "newTodo": [
        {
            "_id": "59fffb068ae3e0b2cd070d1f",
            "text": "Studying",
            "creator": {
                "_id": "59fc257d46900b201d9c1315",
                "username": "johnnyparagon",
                "name": "johnson chinonso"
            },
            "__v": 1,
            "tasks": [
                {
                    "_id": "59fffb278ae3e0b2cd070d20",
                    "text": "newtask",
                    "__v": 0,
                    "createdAt": "2017-11-06T06:01:33.825Z",
                    "task_completer": "",
                    "priority": "normal",
                    "completed": false
                }
            ],
            "collaborators": [
                {
                    "_id": "59fc257d46900b201d9c1315",
                    "username": "johnnyparagon",
                    "name": "johnson chinonso"
                }
            ]
        },
        {
            "_id": "5a002db64a7bfcc2a7908552",
            "text": "newtask",
            "creator": {
                "_id": "59fc257d46900b201d9c1315",
                "username": "johnnyparagon",
                "name": "johnson chinonso"
            },
            "__v": 0,
            "tasks": [],
            "collaborators": [
                {
                    "_id": "59fc257d46900b201d9c1315",
                    "username": "johnnyparagon",
                    "name": "johnson chinonso"
                }
            ]
        },
        {
            "_id": "5a002df54a7bfcc2a7908553",
            "text": "Meditation",
            "creator": {
                "_id": "59fc257d46900b201d9c1315",
                "username": "johnnyparagon",
                "name": "johnson chinonso"
            },
            "__v": 0,
            "tasks": [],
            "collaborators": [
                {
                    "_id": "59fc257d46900b201d9c1315",
                    "username": "johnnyparagon",
                    "name": "johnson chinonso"
                }
            ]
        }
    ]
}
```

## Add Collaborators to Todo

### Request

  * Endpoint: Post: `/api/v1/todos/todoId/collaborator` 
  * Body  `(application/json)` 

### Response
  * Status: `201 created` 
  * Body  `(application/json)` 

> Request:

```json
 {
    "username": "macdoe",
  },

```

> Response:

```json
{
  "success": true,
  "message": "Collaborator have be successfully added"
}

```
## Add task to todo

### Request

  * Endpoint: Post: `/api/v1/todos/todoId/task` 
  * Body  `(application/json)` 

### Response
  * Status: `201 created` 
  * Body  `(application/json)` 

> Request:

```json
 {
    "text": "newTask",
    "priority": "normal"
  },

```
> Response:

```json
{
    "success": true,
    "task": {
        "__v": 0,
        "text": "newtask",
        "_id": "5a002fb54a7bfcc2a7908554",
        "createdAt": "2017-11-06T09:32:29.179Z",
        "priority": "normal",
        "completed": false
    }
}

```
## Retrieve all Tasks that belongs to Todo

### Request

  * Endpoint: Get: `/api/v1/todos/todoId/task` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 

> Response:

```json
{
    "success": true,
    "tasks": [
        {
            "_id": "59fffb278ae3e0b2cd070d20",
            "text": "newtask",
            "__v": 0,
            "createdAt": "2017-11-06T06:01:33.825Z",
            "task_completer": "",
            "priority": "normal",
            "completed": false
        },
        {
            "_id": "5a002fb54a7bfcc2a7908554",
            "text": "newtask",
            "__v": 0,
            "createdAt": "2017-11-06T09:32:29.179Z",
            "task_completer": "",
            "priority": "normal",
            "completed": false
        }
    ]
}

```
## Update task

### Request

  * Endpoint: Put: `/api/v1/todos/todoId/task/taskId` 
  * Body  `(application/json)` 

### Response
  * Status: `201 created` 
  * Body  `(application/json)` 

> Request:

```json
 {
    "completed": true,
  },

```
> Response:

```json
{
    "success": true,
    "editedTask": {
        "_id": "59fffb278ae3e0b2cd070d20",
        "completed": true,
        "__v": 0,
        "createdAt": "2017-11-06T06:01:33.825Z",
        "task_completer": "",
        "priority": "normal"
    }
}

```
## Delete a task

### Request

  * Endpoint: Delete: `/api/v1/todos/todoId/task/taskId` 
  * Body  `(application/json)` 

### Response
  * Status: `200 ok` 
  * Body  `(application/json)` 


> Response:

```json
{
    "success": true,
    "message": "Successfully deleted"
}

```







