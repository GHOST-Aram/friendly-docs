## DELETE `/events/:id`

This allows the client to remove a specific event with the provided ID. Only event organizers can delete event documents. Event organizers are members of the `organizer` user group.

### Authorization
Authentication is needed to access this endpoint. Event documents can only be deleted by the event organizers that own (created) them. If one event organizer tries to delete an event document created by another event organizer, a `Forbidden` response with status `403` will be sent.

Visit [Authentication documentation](../../authentication/auth.md) to learn how to get an authentication token.

### Request
Provide the id of the event document to be deleted as a url parameter as shown below:

```javascript
/events/<eventId>
```

Provide the *authentication token* in the `Authorization` header as Bearer. 

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


### Response
A valid response of a request to this endpoint has a status code `200`. The response body contains the id of the deleted event. The following is an example of the JSON payload contained in the response body:

```json
    "65e449f3a72eaa435166c76c"
```
If the event document to be deleted is not found, a response of status code `404` is sent.
