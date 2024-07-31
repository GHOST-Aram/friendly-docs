## DELETE `/venues/:id`

This endpoint allows clients to remove a specific venue with the provided ID from listings.

### Authorization
Authentication is needed to access this endpoint. Only users of the group `host` can delete venue documents. Venues can only be deleted by the venue hosts that created them. If a venue host tries to delete a document owned (that was created) by another venue host, a `Forbidden` response with status code `403` will be returned. 

Visit [Authentication documentation](../../../authentication/authentication.md) to learn how to get an authentication token.


### Request
Provide the id of the venue document to be deleted as a url parameter an shown below:

```javascript
'/venues/<venueId>'
```

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

    const response = await fetch("<BASE_URL>/venues/65e449f3a72eaa435166c76c", requestOptions)
    
    const body = await response.json()
    console.log('Deleted id: ', body)
})()
```


### Response
A valid response of a request to this endpoint has a status code `200`. The response body contains the id of the deleted venue. The following is an example of the JSON payload contained in the request body.

```json
"65e449f3a72eaa435166c76c"
```

If the event document to be deleted is not found, a response of status code `404` is returned. 