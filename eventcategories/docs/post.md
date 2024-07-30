## POST `/event-categories`

This endpoint allows event organizers and system admins to create a new categories under which events can be grouped. Event organizers and system admins are users of the `organizer` and `superuser` groups respectively.

### Authorization
Only authenticated event organizers or system admins can create an event category. Visit the [authentication docs](../authentication/authentication.md) to acquire an authentication token. Provide the token in the request `Authorization` header as `Bearer`.

### Request
To create a new event category, provide the following event details in the request body:

```typescript
    name: string
    description: string
    graphic?: File
```


**Notes**
- The event graphic is optional but if provided, must be an image file with the extension *.jpg, .jpeg, .png , .avif, or .jfif*
- The description can be any string between 100 and 1000 cahracters in length.

**Examples:**

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

1. POST Request Without an Image File

```javascript

(async() => {
    const data = {`/data object above/`}

    const response = await fetch('<BASE_URL>/event-categories', {
        method: 'POST',
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

2. POST Request with an image File

```javascript

(async() => {
    const formData = {`FormData Object with an image file attached`}

    const response = await fetch('<BASE_URL>/event-categories', {
        method: 'POST',
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

A successful response from this endpoint has the status code of `201`. The response body contains created event category document. The URL of the created item is in the `Location` header of the response object in the format `/event-categories/<eventcategory._id`>.
