# Mesto - backend

## Main route:

https://mesto-api-five.vercel.app/

## Description:

Photo gallery, with the uploading users custom images, registration and likes.
The backend is based on REST-API.
  
## Technologies:
- API: node.js, express, mongodb, mongoose, joi, celebrate, jsonwebtoken

## How to run:

```
npm i
npm run start
```

### Endpoints.

#### Public endpoints:

##### For user registration:
  	
  - POST "/signup". It receive login and password to register a new user account. Beyond that, there are optional values: name, about, avatar. If this are not received, they are assigned default values.
  

  Accepted values are validated for:
   - email, string, required, email verification, repeatability in DB
   - password, string, required, string check
   - name, string, length check (min 2, max 30)
   - about, string, length check (min 2, max 30)
   - avatar, string, url verefication

  After sending request, account information are stored in the database, with hashed password and unique ID, and returned in response.

Request example:
```
    {
      "email": "sipus2006@yandex.ru",
      "password": "qwerty123456"
    }
```
Response example:
```
    {
      "name": "Jacques-Yves Cousteau",
      "about": "Explorer",
      "avatar": "https://pictures.s3.yandex.net/resources/jacques-cousteau_1604399756.png",
      "email": "sipus2006@yandex.ru",
      "_id": "63d57d8ba3fdb2ab7d4ea94c"
    }
```
##### For authentication:
  POST /signin
  
  Takes the login and password for the authentication of an already registered user. Returns a Bearer token.
 
Request example:
```
	{
      "login": "sipus2006@yandex.ru",
      "password": "qwerty123456"
    }
```
Response example:
```
    {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI2M2Q1N2Q4YmEzZmRiMmFiN2Q0ZWE5NGMiLCJpYXQiOjE2NzQ5MzU5NDEsImV4cCI6MTY3NTU0MDc0MX0.Tz0SLJUdn_afkyCGynNDPMpMeUUyufeyX12GnesIip4"
    }
```

#### Private endpoints:
  
  Access requires "Bearer authentication" in "Authorization" header field :
  ```
  "Authorization" : "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI2M2Q1N2Q4YmEzZmRiMmFiN2Q0ZWE5NGMiLCJpYXQiOjE2NzQ5NDE2NTIsImV4cCI6MTY3NTU0NjQ1Mn0.SJFh1w4XIjbHGyexunpynnkUE7iK9Suwkb93D0wzU-0"
  ```

##### For get array with list of all users:
  GET /users

##### For get current user:
  GET /users/me

##### For get user by ID:
  GET /users/:userId

##### For update current user info:
  PATCH /users/me
  
  Only the name and about values can be updated. Both values are required. After sending request, account information are updated in the database and returned in response.
  
##### For update userpic:
  PATCH /users/me/avatar
  
  Update avatar value. The value is validated for URL match.
  
##### For get array of all cards:
  GET /cards
  
##### For post new card:
  POST /cards
  
  Accepts "name" and "link" values. After sending request, account information are stored in the database, with unique ID, owner ID, and returned in response.
  
  Accepted values are validated for:
   - name, string, required, length check (min 2, max 30)
   - link, string, required, url verefication
 

Request example:
```
    {
      "name": "Universidad de Madrid",
      "link": "https://upload.wikimedia.org/wikipedia/commons/3/31/Rectorado_de_la_Universidad_Complutense_de_Madrid.jpg"
    }
```
Response example:
```
    {
      "name": "Universidad de Madrid",
      "link": "https://upload.wikimedia.org/wikipedia/commons/3/31/Rectorado_de_la_Universidad_Complutense_de_Madrid.jpg",
      "owner": "63d57d8ba3fdb2ab7d4ea94c",
      "likes": [],
      "_id": "63d5b1c8a3fdb2ab7d4ea95b",
      "createdAt": "2023-01-28T23:37:44.048Z",
      "__v": 0
    }
```

##### For post delete card:
  DELETE /cards/:cardId
  
  Card can delete only card owner. After sending request, card information are delete from the database and returned in response.
  
##### For put like on card:
  PUT /cards/:cardId/likes
  
  After sending request, card information are updated in the database and returned in response.
  

##### For delet like from card:
  DELETE /cards/:cardId/likes
  
  After sending request, card information are updated in the database and returned in response.
