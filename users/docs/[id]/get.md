## GET users/:id

This endpoint makes allows you to retrieve user details using a specified user ID.

### Authorization
User details can only be read by an authenticated user. An authenticated user can read the details of any other user in the system. 

Visit the [authentication documentation](../../authentication/authentication.md) to learn how to get an authorization token.

### Request
Provide the target user id as a url parameter in the request url as shown below to fetch the details:

```javascript
/users/<userId>
```

Provide the *authentication token* in the `Authorization` header of the request as Bearer to authenticate the request.

**Example**
```javascript
(async() =>{
    const response =  await fetch('<BASE_URL>/users/65e40da5c390b114451cebb5',{
        method: 'GET',
        headers:{
            'Authorization': 'Bearer <Authorization token>'
        }
    })

    const body = await response.json()
    console.log(body)
})()
```

### Response
A successful response sent from this endpoint has a status code of `200`. The user details are contaied in the response body as a json payload. The following is an example of a user object contained in the response body as a JSON payload.

```json
{
    "_id": "65e40da5c390b114451cebb5",
    "fullName": "Curtis Jackson",
    "userGroup": "superuser",
    "email": "Nyasia.Kreiger@gmail.com",
    "password": "$2b$10$NkE10T4T8zCVvIawiFHkb.MRV19Nstb9do.aD58pGAaq.um1aPa4i",
    "__v": 1
}
```
If the document to be fetched is not, a response with status code of `404` is sent.