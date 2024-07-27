## PATCH `/event-categories`

This endpoint allows event organizers and system admins to modify details of an event category. Event organizers and system admins are users of the `organizer` and `superuser` groups respectively.

### Authorization
Only authenticated event organizers or system admins can modify an Event Category. 

Admins or event organizers can only update documents they created. If an admin tries to update a document created by another admin or an event organizer, the server will deny the request and respond with status code `403` (Forbidden). Same goes for event organizers.

Visit the [authentication docs](../authentication/authentication.md) to acquire authentication token. Provide the token in the request `Authorization` header as `Bearer`.


### Request
To update a new event, provide the following event details in the request body:

```typescript
    name: string
    description: string
    graphic?: File
```


**Notes**
- The event graphic is optional but if provided, must be an image file with the extension *.jpg, .jpeg, .png , .avif, or .jfif*
- The description can be any string between 100 and 1000 cahracters in length.

### Response

A successful response from this endpoint has the status code of `200`. The response body contains modified document. The URL to the modified item is in the `Location` header of the response object in the format `/event-categories/<eventCategory._id`>. If the document to be modified does not exist, a response with status code of `404` is sent.


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

1. PATCH Request Without an Image File

```javascript

(async() => {
    const data = {`/data object above/`}

    const response = await fetch('<BASE_URL>/event-categories', {
        method: 'PATCH',
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

2. PATCH Request with an image File

```javascript

(async() => {
    const formData = {`FormData Object with an image file attached`}

    const response = await fetch('<BASE_URL>/event-categories', {
        method: 'PATCH',
        body: formData,
        headers:{
            'Authorization': 'Bearer <token>'
        }
    })

    const body = await response.json()

    console.log('Event Category Data: ', body)
})()
```