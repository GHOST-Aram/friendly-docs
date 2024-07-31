## GET /users

This endpoint allows the client to retrieve a list of users that are registered with the system. 

The response returns a paginated list by default, the default pagination limit is 10, you can change this value using query parameters.


## Authorization
Only authenticated users with admin rights (superusers) can read the list of all users. Visit the [authentication documentation](../authentication/auth.md) to find out how to get an authorization token.

### Request
You can send a request to view list of users with the desired pagination constraints or without pagination constraints. If the request does not include client defined constraints, the system will use it's default pagination constraints to process the request. Pagination constraints can be defined using the following query parameters:

- `page`: number
- `limit`: number

Pagination constraints can be included in the url as shown in the following URL

```t
/users?page=2&&limit=21
```

**Example**

```javascript
(asyn() =>{

    const response = await fetch('<BASE_URL>/users', {
        method: 'GET',
        headers: {
            'Authorization': 'Bearer<token>'
        }
    })

    const body = await response.json()

    console.log('Users: ', body)
})()
 ```


### Response
A success response from this endpoint has a status code of `200`. The list of users is contained in the response body as a JSON payload. The following is an example of response body content.

```json
[
    {
    "_id": "669e526fa9ed3824e6db45b9",
    "fullName": "Darlene Hills",
    "userGroup": "superuser",
    "email": "RafaelBergnaum@gmail.com",
    "password": "$2b$10$NkE10T4T8zCVvIawiFHkb.MRV19Nstb9do.aD5fewer.um1aPa4i",
    "__v": 0
},
{
    "_id": "669e526fa9ed3824e6db2db9",
    "fullName": "Darlene Hills",
    "userGroup": "superuser",
    "email": "RafaelBergnaum@yahoo.com",
    "password": "$2b$10$NkE10T4T8zCVvIawiFHkb.MRV19Nstb9do.aD58pGAaq.um1aPa4i",
    "__v": 0
}
]
```