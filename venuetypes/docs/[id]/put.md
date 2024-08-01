## PUT `/venue-types`

This endpoint allows system admins and venue hosts ( VENUE managers/owners/landlords) to update venue types. Venue hosts and system admins are users of the `host` and `superuser` groups respectively.

### Authorization
Only authenticated venue hosts and system admins can update venue types.  Admins or hosts can only update documents they created. If an admin tries to update a document created by another admin or another venue host, the server will deny the request and respond with status code `403` (Fobbiden). Same goes for venue hosts.

Visit the [authentication docs](../../../authentication/authentication.md) to acquire an authentication token. Provide the token in the request `Authorization` header as `Bearer`.

### Request
To update an venue types via PUT method, provide the following venue details in the request:

```typescript
   {
    name: string
    description: string
}
```

**Notes**
- The description should be a string of not less than 100 characters and not more than 1000 characters in length.

**Example:**

```javascript
(async() => {

    const data = {
        name: "Sports Stadium",
        
        description: `
            Lorem ipsum dolor sit, amet consectetur adipisicing elit. 
            Maiores libero illo praesentium autem nesciunt consectetur 
            repudiandae omnis eum similique in, quas rerum. Eveniet, 
            possimus doloremque?
        `,
    }

    const response = await fetch('<BASE_URL>/venue-types', {
        method: 'PUT',
        body: JSON.stringify(data),
        headers:{
            'Content-Type': 'application/json',
            'Authorization': 'Bearer <token>'
        }
    })

    const body = await response.json()

    console.log('venue type: ', body)
})()
```


### Response

A successful response from this endpoint has the status code of `200`. The URL of the updated or created item is in the `Location` header of the response object in the format `/venue-types/<venueType._id`>. The response body contains updated venue type document. The following is an example of the JSON payload contained in the response body.

```json
{
    "_id": "66ab81ff64f0899f1d8a3980",
    "name": "Olympics Stadium",
    "description": "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Maiores libero illo praesentium autem nesciunt consectetur repudiandae omnis eum similique in, quas rerum. Eveniet, possimus doloremque?",
    "createdBy": "66aa43ae6e3b901410065479",
    "__v": 0
}
```

If the document to be updated does not exist, a new document is created and a response with status code of `201` is sent.
