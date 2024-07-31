## PUT `/venue-types`

This endpoint allows system admins and venue hosts (venue managers/owners/landlords) to modify venue types. Venue hosts and system admins are users of the `host` and `superuser` groups respectively. 

### Authorization
Only authenticated venue hosts and system admins can modify venue types. Admins or hosts can only modify documents they created. If an admin tries to modify a document created by another admin or any venue host, the server will deny the request and respond with status code `403` (Fobbiden). Same goes for venue hosts.

Visit the [authentication docs](../authentication/authentication.md) to acquire authentication token. Provide the token in the request `Authorization` header as `Bearer`.

### Request
To modify an venue types via PATCH method, provide any or all of the following venue details in the request:

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

A successful response from this endpoint has the status code of `200`. The URL to the modified item is in the `Location` header of the response object in the format `/venue-types/<venueType._id`>. The response body contains modified venue type document. The following is an example of the JSON payload contained in the response body:

```json

```

If the document to be modified is not found, a response with status code of `404` is sent.
