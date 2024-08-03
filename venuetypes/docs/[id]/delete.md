## DELETE `/venue-types/:id`

This endpoint allows system admins and venue hosts to remove a specific venue type with a specified ID. Venue hosts and system admins are users of the `host` and `superuser` groups respectively. 

### Authorization
Only authenticated venue hosts and admins can delete venue types. A venue type can only be deleted by its creator. If an admin tries to delete a document created by another admin or any venue host, the server will deny the request and respond with status code `403` (Forbidden).

Visit [Authentication documentation](../../../authentication/authentication.md) to learn how to get an authentication token. Provide the auth token in the `Authorization` header as Bearer. 

### Request
To delete the details of a venue type, provide the ID of the venue as a URL parameter. 
```javascript
    '<BASE_URL>/venue-types/65e449f3a72eaa435166c76c'
```

**Example:**

```javascript
    (async() =>{
        const myHeaders = new Headers();
        myHeaders.append("Authorization", "Bearer <token>");

        const requestOptions = {
            method: "DELETE",
            headers: myHeaders,
    };

    const response = await fetch("<BASE_URL>/venue-types/65e449f3a72eaa435166c76c",     requestOptions)
        
        const body = await response.json()
        console.log('Deleted id: ', body)
    })()
```


### Response
A valid response of a request to this endpoint has a status code `200`. The response body contains the ID of the deleted venue type. The following is an example of the JSON payload in the response body.

```json
    "66ab81ff64f0899f1d8a3980"
```

If the target document to be deleted is not found, a response of status code `404` is sent.
