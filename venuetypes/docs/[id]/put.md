## PUT `/venue-types`

This endpoint allows system admins and venue hosts (managers/owners/landlords) to update venue types.

### Authorization
Only authenticated venue hosts and system admins can update venue types. Venue hosts and system admins are users of the `host` and `superuser` groups respectively. 

Admins or hosts can only update documents they created. If an admin tries to update a document created by another admin or another venue host, the server will deny the request and respond with status code `403` (Fobbiden). Same goes for venue hosts.

Visit the [authentication docs](../authentication/authentication.md) to acquire authentication token. Provide the token in the request `Authorization` header as `Bearer`.

### Request
To update an venue types via PUT method, provide the following venue details in the request:

```typescript
   {
    name: string
    description: string
}
```

The description should be a string of not less than 100 characters and not more than 1000 characters in length.


### Response

A successful response from this endpoint has the status code of `200`. If the document to be updated does not exist, a new document is created and a response with status code of `201` is sent. The response body contains updated venue type document. The URL of the updated or created item is in the `Location` header of the response object in the format `/venue-types/<venueType._id`>.


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