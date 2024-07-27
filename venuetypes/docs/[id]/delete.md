## DELETE `/venue-types/:id`

This endpoint allows system admins and venue hosts to remove a specific venue type with a specified ID. A venue type can only be deleted by its creator. If an admin tries to delete a document created by another admin or any venue host, the server will deny the request and respond with status code `403` (Fobbiden)

### Authorization
Authentication is needed to access this endpoint. Only users of the group `host` or `superuser` can delete venue types. Visit [Authentication documentation](../../../authentication/authentication.md) to learn how to get an authentication token.

### Request
To delete the details of a venue type, provide the id of the venue as a url parameter. 
```javascript
    '<BASE_URL>/venue-types/65e449f3a72eaa435166c76c'
```

Provide the auth token in the `Authorization` header as Bearer. 

### Response
A valid response of a request to this endpoint has a status code `200`. If the target of deletion is not found, a response of status code `404` is received. The response body contains the id of the deleted venue type.

**Example:**

```javascript
(async() =>{
    const myHeaders = new Headers();
    myHeaders.append("Authorization", "Bearer <token>");

    const requestOptions = {
        method: "DELETE",
        headers: myHeaders,
    };

    const response = await fetch("<BASE_URL>/venue-types/65e449f3a72eaa435166c76c", requestOptions)
    
    const body = await response.json()
    console.log('Deleted id: ', body)
})()
```
