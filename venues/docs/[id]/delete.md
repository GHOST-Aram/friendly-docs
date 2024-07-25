## DELETE `/venues/:id`

This endpoint sends a HTTP DELETE request to remove a specific venue with the provided ID.

### Authorization
Authentication is needed to access this endpoint. Only users of the group `host` can delete venue documents. venues can only be deleted by the venue owners/managers/landlords that created them.  Visit [Authentication documentation](../../../authentication/authentication.md) to learn how to get an authentication token.

### Request
To delete the details of a venue, provide the id of the venue as a url parameter. Provide the token in the `Authorization` header as Bearer. 

### Response
A valid response of a request to this endpoint has a status code `200`. If the target of deletion is not found, a response of status code `404` is received. The response body contains the id of the deleted venue.

**Example:**

```javascript
(async() =>{
    const myHeaders = new Headers();
    myHeaders.append("Authorization", "Bearer <token>");

    const requestOptions = {
        method: "DELETE",
        headers: myHeaders,
    };

    const response = await fetch("<BASE_URL>/venues/65e449f3a72eaa435166c76c", requestOptions)
    
    const body = await response.json()
    console.log('Deleted id: ', body)
})()
```
