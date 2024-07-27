## POST `/venue-types`

This endpoint allows admins and venue hosts (managers/owners/landlords) to create categories of venues. Venues can be anything from stadium, theatre, cinema hall etc. Its important to have them grouped under various types in the system.

### Authorization
Only authenticated venue hosts and system admins can create venue types. Venue hosts and system admins are users of the `host` and `superuser` user groups respectively. Visit the [authentication docs](../authentication/authentication.md) to acquire authentication token. Provide the token in the request `Authorization` header as `Bearer`.

### Request
The venue types POST request handler expects data of the following shape in the request body:

```typescript
   {
    name: string
    description: string
}
```

The description should be a string of not less than 100 characters and not more than 1000 characters in length.


### Response

A successful response from this endpoint has the status code of `201`. The response body contains created venue document. The URL of the created item is in the `Location` header of the response object in the format `/venue-types/<venueType._id`>.


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