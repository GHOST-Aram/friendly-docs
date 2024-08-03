## GET /users

This endpoint allows the client to retrieve a list of users that are registered with the system. The response returns a paginated list by default, the default pagination limit is 10, you can change this value using query parameters.


## Authorization
Only authenticated users with admin rights (superusers) can read the list of all users. Visit the [authentication documentation](../authentication/auth.md) to find out how to get an authorization token.

### Request
You can send a request to fetch a list of users with the desired pagination constraints or without pagination constraints. Pagination constraints can be defined using the following query parameters:

- `page`: number
- `limit`: number

Pagination constraints can be included in the URL as shown in the following URL

```javascript
'/users?page=2&&limit=21'
```

If the request does not include client-defined constraints, the system will use its default pagination constraints to process the request.

**Example**

```javascript
(async() =>{

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
A successful response from this endpoint has a status code of `200`. The list of users is contained in the response body as a JSON payload. The following is an example of response body content.

```json
[
 {
        "_id": "66aa425d6e3b901410065476",
        "fullName": "Darlene Hills",
        "userGroup": "superuser",
        "email": "RafaelBergnaum@erd.edu",
        "__v": 0
 },
 {
        "_id": "66aa43ae6e3b901410065479",
        "fullName": "Darlene Hills",
        "userGroup": "host",
        "email": "host_Bergnaum5@gmail.com",
        "__v": 0
 },
]
```