## DELETE `/users/:id`

This endpoint allows the client to remove a specific user with the provided ID.


### Authorization
Only authenticated users can delete user documents. Users can only delete their own details and not the details of other users. If a user tries to update a document owned by another user, a `Forbidden` response with status code `403` will be received. 

Visit [Authentication documentation](../../../authentication/authentication.md) to learn how to get an authentication token.


### Request
Provide the ID of the user to be deleted as a URL parameter as shown below. 

```javascript
/users/<userId>
```

The ID must be the same as the ID of the authenticated user sending the request, this is because users can only be allowed to delete their own information. 

Provide the *authentication token* in the `Authorization` header as Bearer to authenticate the request. 

**Example:**

```javascript
(async() =>{
    const myHeaders = new Headers();
    myHeaders.append("Authorization", "Bearer <token>");

    const requestOptions = {
        method: "DELETE",
        headers: myHeaders,
 };

    const response = await fetch("http://localhost:8000/users/65e449f3a72eaa435166c76c", requestOptions)
    
    const body = await response.json()
    console.log('Deleted id: ', body)
})()
```

### Response
A successful response from this endpoint has a status code `200`. The response body contains the ID of the deleted user document as a JSON payload. The following is an example of the JSON payload contained in the response body:

```json
    "65e449f3a72eaa435166c76c"
```

If the user document to delete is not found, a response with the status code `404` is received.