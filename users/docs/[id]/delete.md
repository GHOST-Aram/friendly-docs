## DELETE `/users/:id`

This endpoint allows the client to remove a specific user with the provided ID.


### Authorization
Authentication is needed to access this endpoint. Users can only delete their own details and not details of other users. If a user tries to update a document owned by another user, a `Forbidden 403` response will be received. 

Visit [Authentication documentation](../../authentication/auth.md) to learn how to get an authentication token.


### Request
To delete the details of a user, provide the id of the user as a url parameter. The id must be the same as the id of the authenticated user sending the request, this is because users can only be allowed to delete their own information. 

Provide the token in the `Authorization` header as Bearer. 

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
A valid response of a request to this endpoint has a status code 200. If the target of deletion is not found, a response of status code `404` is received. The response body contains the  the id of the deleted user as in the example below.

```json
    "65e449f3a72eaa435166c76c"
```