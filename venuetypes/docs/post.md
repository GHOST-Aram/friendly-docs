## POST `/venue-types`

This endpoint allows admins and venue hosts (managers/owners/landlords) to create categories under which venues can be grouped. Venue hosts and system admins are users of the `host` and `superuser` user groups respectively.

### Authorization
Only authenticated venue hosts and system admins can create venue types. Visit the [authentication docs](../authentication/authentication.md) to acquire an authentication token. Provide the token in the request `Authorization` header as `Bearer`.

### Request
The venue types POST request handler expects data of the following shape in the request body:

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
        method: 'POST',
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
A successful response from this endpoint has the status code of `201`. The URL of the created item is in the `Location` header of the response object in the format `/venue-types/<venueType._id`>. The response body contains created venue document. The following is an example of the JSON payload contained in the response body.

```json
{
    "name": "Sports Center&#x2F;Stadium",
    "description": "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Maiores libero illo   praesentium autem nesciunt consectetur repudiandae omnis eum similique in, quas rerum. Eveniet, possimus doloremque?",
    "createdBy": "66aa43ae6e3b901410065479",
    "_id": "66ab81ff64f0899f1d8a3980",
    "__v": 0
}
```