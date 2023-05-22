
# Contact API

This is simple REST API Contact project. 


## Installation

Install project with npm

```bash
  npm install 

```

## Run

Run project with npm

```bash
  npm start  

```
    
## API Reference 


### Singup

```http
  POST /api/users/singup
```

#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Body| `email` | `string` | **Required**.  Email address |
| Body | `password` | `string` | **Required**.  Password |



#### Response

| Status | Description                |
| :-------- |  :------------------------- |
| `400` |  Bad request (email or password has not passed validation ) |
| `409` |  Email is alredy taken |
| `500` |  Server errors  |
| `201` |  New account is created. Account isn't verify yet. A verified link has been sent  to the provided e-mail  address  |

 
 ####  Respone Body Example:
 

 
```json
{
    "id": "user.id",
    "email": "user.emial",
    "subscription": "user.subscription",
}
```
or

```json
{
    "message": "error message",
}
```


### Login

```http
  POST /api/users/login
```

#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Body| `email` | `string` | **Required**.  Email address |
| Body | `password` | `string` | **Required**.  Password |

 ####  Respone 

| Status | Description                |
| :-------- |  :------------------------- |
| `400` |  Bad request (email or password has not passed validation; User doesn`t exist  ) |
| `401` |  Unauthorized (Email or posswors isn't correct; User isn't verify)  |
| `500` |  Server errors  |
| `200` |  Login. |


 #### Response Body Example:


```json
{
    "token" : "JWT"
    "user:":
            {
                "id": "user.id",
                "email": "user.emial",
                "subscription": "user.subscription",
             }
}
```
or

```json
{
    "message": "error message",
}
```


### Logout

```http
  GET /api/users/logout
```

#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Header | `Authorization` | `JWT` | **Required**.  JWT Bearer |


#### Response

| Status | Description                |
| :-------- |  :------------------------- |
| `204` |  Logout |
| `500` |  Server errors  |


 #### Response Body Example:
 

 
```json
{
    "email": "user.emial",
    "subscription": "user.subscription",
}
```
or

```json
{
    "message": "error message",
}
```



### Current

```http
  GET /api/users/current
```

#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Header | `Authorization` | `JWT` | **Required**.  JWT Bearer |


#### Response

| Status | Description                |
| :-------- |  :------------------------- |
| `200` |  Current user is returned in request body  |
| `401` |  Unauthorized   |
| `500` |  Server errors  |


 #### Response Body Example:
 

 
```json
{
    "email": "user.emial",
    "subscription": "user.subscription",
}
```
or

```json
{
    "message": "error message",
,
}
```

### Update subscription

```http
  Patch /api/users/
```
#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Header | `Authorization` | `JWT` | **Required**.  JWT Bearer |
| Body | `subscription` | `String` | **Required**.  Type of subscription |



#### Response

| Status | Description                |
| :-------- |  :------------------------- |
| `200` |  Subscription has been update succesful |
| `400` |  Bad request (subscription isn't verified) |
| `401` |  Unauthorized   |
| `500` |  Server errors  |



 #### Response Body Example:
 

 
```json
{
    "email": "user.emial",
    "subscription": "user.subscription",
}
```
or

```json
{
    "message": "error message",
}
```

### Update avatars

```http
  Patch /api/users/avatars
```
#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Header | `Authorization` | `JWT` | **Required**.  JWT Bearer |
| Body | `avatar` | `file` | **Required**.  New avatar |


#### Response

| Status | Description                |
| :-------- |  :------------------------- |
| `200` |  Avatar has been update succesful |
| `401` |  Unauthorized   |
| `500` |  Server errors  |



 #### Response Body Example:
 

 
```json
{
    "avatarURL": "path to avatar",
}
```
or

```json
{
    "message": "error message",
}
```


### Re-verification

```http
  post /api/users/verify
```


#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Body | `email` | `String` | **Required**.  Email address |

#### Response

| Status | Description                |
| :-------- |  :------------------------- |
| `400` |  Bad request (email isn't validation;  missing field email; Verifiacaiont has alredy been passed ) |
| `404` |  User isn't exist |
| `200` |  A verified link has been  again sent  to the provided e-mail  address  |
| `500` |  Server errors  |



 #### Response Body Example:
 

 
```json
{
    "message": "message",
}
```


### Get all contacts

```http
  GET /api/contacts/page=number&limit=numberfavorite=boolean

```
#### Parameter 
 |Parameter |  Description                |
 |:-------- | :------------------------- |
 |`Limit` |  The number of results to return per page. Default is of Infinite  |
 |`Page` |  Use this to page through the results. |
 |`Favorite` | Sort by favourite flag  |


#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Header | `Authorization` | `JWT` | **Required**.  JWT Bearer |

 ####  Respone 

| Status | Description                |
| :-------- |  :------------------------- |
| `401` |  Unauthorized   |
| `500` |  Server errors  |
| `200` |   Array of contacts is retrned in request body |


 #### Response Body Example:


```json
[
    {
        "_id": "6442f74bc5585313a483dccd",
        "name": "Allen Raymond",
        "email": "nulla.ante@vestibul.co.uk",
        "phone": "(992) 914-3792",
        "favorite": false,
        "owner": "6442be4b4fb8f585c6f14102" 
    },
]


```
or

```json
{
    "message": "error message",
}
```

### Get contact by id

```http
  GET /api/contacts/:contactId

```
#### Parameter 
 |Parameter |  Description                |
 |:-------- | :------------------------- |
 |`id` |  The id of contact  |
 


#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Header | `Authorization` | `JWT` | **Required**.  JWT Bearer |

 ####  Respone 

| Status | Description                |
| :-------- |  :------------------------- |
| `401` |  Unauthorized   |
| `404` |  Contact with provided id doesn't exist   |
| `500` |  Server errors  |
| `200` |   Array of contacts is retrned in request body |


 #### Response Body Example:


```json

    {
        "_id": "6442f74bc5585313a483dccd",
        "name": "Allen Raymond",
        "email": "nulla.ante@vestibul.co.uk",
        "phone": "(992) 914-3792",
        "favorite": false,
        "owner": "6442be4b4fb8f585c6f14102" 
    }



```
or

```json
{
    "message": "error message",
}
```


### Create contact

```http
  POST /api/contacts

```



#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Header | `Authorization` | `JWT` | **Required**.  JWT Bearer |
| Body | `email` | `String` | **Required**.  Email address of new contact|
| Body | `phone` | `String` | **Required**.  Phone number of new contact |
| Body | `name` | `String` | **Required**.  Name  of of new contact |



 ####  Respone 

| Status | Description                |
| :-------- |  :------------------------- |
| `401` |  Unauthorized   |
| `400` |  Bad request (missing field; Parameter isn't validate)   |
| `500` |  Server errors  |
| `201` |  New contact has been created |




 #### Response Body Example:


```json

    {
        "_id": "6442f74bc5585313a483dccd",
        "name": "Allen Raymond",
        "email": "nulla.ante@vestibul.co.uk",
        "phone": "(992) 914-3792",
        "favorite": false,
        "owner": "6442be4b4fb8f585c6f14102" 
    }



```
or

```json
{
    "message": "error message",
}
```

### Delete contact

```http
  DELETE /api/contacts:contactId

```
#### Parameter 
 |Parameter |  Description                |
 |:-------- | :------------------------- |
 |`id` |  The id of contact  |

#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Header | `Authorization` | `JWT` | **Required**.  JWT Bearer |


 ####  Respone 

| Status | Description                |
| :-------- |  :------------------------- |
| `401` |  Unauthorized   |
| `404` |  Contact with provided id doesn't exist  |
| `500` |  Server errors  |
| `201` |  Contact has been deleted |




 #### Response Body Example:


```json

    {
         "message": "contact has been deleted",
    }



```
or

```json
{
    "message": "error message",
}
```


### Update contact

```http
  PUT /api/contacts:contactId

```

#### Parameter 
 |Parameter |  Description                |
 |:-------- | :------------------------- |
 |`id` |  The id of contact  |


#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Header | `Authorization` | `JWT` | **Required**.  JWT Bearer |
| Body | `email` | `String` |  Email address of new contact|
| Body | `phone` | `String` |  Phone number of new contact |
| Body | `name` | `String` |   Name  of of new contact |

Only oe parameter in request body is **Required**

 ####  Respone 

| Status | Description                |
| :-------- |  :------------------------- |
| `401` |  Unauthorized   |
| `400` |  Bad request (missing field; Parameter isn't validate)   |
| `500` |  Server errors  |
| `200` |  Contact has been updated |


 #### Response Body Example:


```json

   {
    "_id": "6442f74bc5585313a483dccd",
    "name": "Allen Raymond",
    "email": "nulla.ante@vestibul.co.uk",
    "phone": "(715) 598-5792",
    "favorite": false,
    "owner": "6442be4b4fb8f585c6f14102"
}



```
or

```json
{
    "message": "error message",
}
```



### Update favorite field

```http
  PUT /api/contacts:contactId/favorite

```

#### Parameter 
 |Parameter |  Description                |
 |:-------- | :------------------------- |
 |`id` |  The id of contact  |


#### Request 
|Structure | Parameter | Type     | Description                |
| :-------- | :-------- | :------- | :------------------------- |
| Header | `Authorization` | `JWT` | **Required**.  JWT Bearer |
| Body | `favorite` | `boolean` | **Required**.   Favorite parmeter |


On

 ####  Respone 

| Status | Description                |
| :-------- |  :------------------------- |
| `401` |  Unauthorized   |
| `404` |  Contact with provided id doesn't exist  |
| `400` |  Bad request (missing field; Parameter isn't validate)   |
| `500` |  Server errors  |
| `200` |  Field favorite has been updated |


 #### Response Body Example:


```json

   {
    "_id": "6442f74bc5585313a483dccd",
    "name": "Allen Raymond",
    "email": "nulla.ante@vestibul.co.uk",
    "phone": "(715) 598-5792",
    "favorite": false,
    "owner": "6442be4b4fb8f585c6f14102"
}



```
or

```json
{
    "message": "error message",
}
```
