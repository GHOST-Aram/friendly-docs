## DELETE `/event-categories/:id`

This endpoint allows system admins and event organizers to remove a specific event category from the system. Event organizers and system admins are users of the `organizer` and `superuser` groups respectively. 

### Authorization
Only authenticated event organizers or system admins can delete an event category. An event category can only be deleted by its creator. If an admin tries to delete a document created by another admin or any event organizer, the server will deny the request and respond with status code `403` (Forbidden). The vice versa is true.

Visit [Authentication documentation](../../../authentication/authentication.md) to learn how to get an authentication token.


### Request
Provide the ID of the target venue category as a URL parameter as shown below to send a delete request. 

```javascript
    '<BASE_URL>/event-categories/65e449f3a72eaa435166c76c'
```

Provide the *authentication token* in the request `Authorization` header as `Bearer`.

**Example:**

```javascript
(async() =>{
    const myHeaders = new Headers();
    myHeaders.append("Authorization", "Bearer <token>");

    const requestOptions = {
        method: "DELETE",
        headers: myHeaders,
 };

    const response = await fetch("<BASE_URL>/event-categories/65e449f3a72eaa435166c76c", requestOptions)
    
    const body = await response.json()
    console.log('Deleted id: ', body)
})()
```

### Response
A valid response of a request to this endpoint has a status code `200`. The response body contains the ID of the deleted event category. The following is an example of the JSON payload contained in the response body:

```json
"65e449f3a72eaa435166c76c"
```

If the document to be deleted is not found, a response with the status code `404` is returned.