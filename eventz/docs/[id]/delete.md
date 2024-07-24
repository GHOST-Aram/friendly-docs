## DELETE `/events/:id`

This endpoint sends a HTTP DELETE request to remove a specific event with the provided ID.

### Authorization
Authentication is needed to access this endpoint. Only users of the group `organizer` can delete event documents. Events can only be deleted by the event organizers that created them.  Visit [Authentication documentation](../../authentication/auth.md) to learn how to get an authentication token.

### Request
To delete the details of a event, provide the id of the event as a url parameter. Provide the token in the `Authorization` header as Bearer. 

### Response
A valid response of a request to this endpoint has a status code `200`. If the target of deletion is not found, a response of status code `404` is received. The response body contains the id of the deleted event.

**Example:**

```javascript
(async() =>{
    const myHeaders = new Headers();
    myHeaders.append("Authorization", "Bearer <token>");

    const requestOptions = {
        method: "DELETE",
        headers: myHeaders,
    };

    const response = await fetch("<BASE_URL>/events/65e449f3a72eaa435166c76c", requestOptions)
    
    const body = await response.json()
    console.log('Deleted id: ', body)
})()
```
