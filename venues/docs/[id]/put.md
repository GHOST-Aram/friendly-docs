## PUT `/venues`

This endpoint allows venue managers/owners/landlords to create a new venue.

### Authorization
Only authenticated venue managers/owners/landlords can update venues. Venue managers/owners/landlords are users of the `host` user group. Visit the [authentication docs](../authentication/authentication.md) to acquire authentication token. Provide the token in the request `Authorization` header as `Bearer`.

### Request
To update an venue via PUT method, provide the following venue details in the request:

```typescript

    type: string
    name: string
    capacity: number
    address: {
        cityOrTown: string
        street: string
        block: {
            name: string,
            floor: number
        }
    }
    pictures?: File[]
    description: string
    accessibilityFeatures: {
        stairCase: boolean,
        elevator: boolean,
        escallator: boolean,
        ramp: boolean
    }
    coordinates: {
        latitude: number
        longitude: number
    }

```


### Response

A successful response from this endpoint has the status code of `200`. If the document to be updated does not exist, a new document is created and a response with status code of `201` is sent. The response body contains updated venue document. The URL of the created item is in the `Location` header of the response object in the format `/venues/<venue._id`>.


Example:

  ```javascript
    const data = {
        type: "5 star Hotel",
        name: "Paradise Eden",
        capacity: 20000,
        address: {
            cityOrTown: 'Nairobi',
            street: '34 North',
            block: {
                name: "Paradise Building",
                floor: 4,
            }
        },
        description: `
            Lorem ipsum dolor sit, amet consectetur adipisicing elit. 
            Maiores libero illo praesentium autem nesciunt consectetur 
            repudiandae omnis eum similique in, quas rerum. Eveniet, 
            possimus doloremque?
        `,
        accessibilityFeatures: {
            stairCase: true,
            elevator: true,
            escallator: false,
            ramp: true
        },
        coordinates: {
            latitude: -36.3,
            longitude: -12.5
        }
    }
```

1. PUT Request Without an Image File

```javascript

(async() => {
    const data = {`/data object above/`}

    const response = await fetch('<BASE_URL>/venues', {
        method: 'PUT',
        body: JSON.stringify(data),
        headers:{
            'Content-Type': 'application/json',
            'Authorization': 'Bearer <token>'
        }
    })

    const body = await response.json()

    console.log('venue: ', body)
})()
```

2. PUT Request with venue pictures

```javascript

(async() => {
    const formData = {`FormData Object with venue pictures attached`}

    const response = await fetch('<BASE_URL>/venues', {
        method: 'PUT',
        body: formData,
        headers:{
            'Authorization': 'Bearer <token>'
        }
    })

    const body = await response.json()

    console.log('venue: ', body)
})()
```