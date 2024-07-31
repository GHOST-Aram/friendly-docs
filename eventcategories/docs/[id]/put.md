## PUT `/event-categories`

This endpoint allows event organizers and system admins to update the details of an event category. Event organizers and system admins are users of the `organizer` and `superuser` groups respectively.

### Authorization
Only authenticated event organizers or system admins can update an Event Category. Admins or event organizers can only update documents they created. If an admin tries to update a document created by another admin or another event organizer, the server will deny the request and respond with status code `403` (Fobbiden). Same goes for event organizers.

Visit the [authentication docs](../authentication/authentication.md) to acquire authentication token. Provide the token in the request `Authorization` header as `Bearer`.

### Request
To update a new event category, provide the following event details in the request body:

```typescript
    name: string
    description: string
    graphic?: File
```


**Notes**
- The event graphic is optional but if provided, must be an image file with the extension *.jpg, .jpeg, .png , .avif, or .jfif*
- The description can be any string between 100 and 1000 cahracters in length.

**Example:**

  ```javascript
    const data = {
        name: "Music Concert"  ,
        description: `
            Lorem ipsum dolor sit amet consectetur adipisicing elit. 
            Nam libero incidunt deleniti iusto facere, vero ducimus 
            ex totam eius dolores.vero ducimus ex totam eius dolores.
        `
    }
```

1. PUT Request Without an Image File

```javascript

(async() => {
    const data = {`/data object above/`}

    const response = await fetch('<BASE_URL>/event-categories', {
        method: 'PUT',
        body: JSON.stringify(data),
        headers:{
            'Content-Type': 'application/json',
            'Authorization': 'Bearer <token>'
        }
    })

    const body = await response.json()

    console.log('Event Category Data: ', body)
})()
```

2. PUT Request with an image File

```javascript

(async() => {
    const formData = {`FormData Object with an image file attached`}

    const response = await fetch('<BASE_URL>/event-categories', {
        method: 'PUT',
        body: formData,
        headers:{
            'Authorization': 'Bearer <token>'
        }
    })

    const body = await response.json()

    console.log('Event Category Data: ', body)
})()
```

### Response

A successful response from this endpoint has the status code of `200`. The URL of the updated item is in the `Location` header of the response object in the format `/event-categories/<eventCategory._id`>. The response body contains updated event category document. 

The following is an example of the JSON payload contained in the response body:

```json

```

If the document to be updated does not exist, a new document is created and a response with status code of `201` is returned.