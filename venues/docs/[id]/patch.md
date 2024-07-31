## PATCH `/venues`

This endpoint allows venue hosts ( venue managers/owners/landlords) to modify venue information.  Venue hosts are users of the `host` user group.

### Authorization
Only authenticated venue hosts can modify venues. A venue host can only update a document they own. If a venue host tries to update a document owned (was created) by another venue host, a `Forbidden 403` response will be received.

Visit the [authentication docs](../authentication/authentication.md) to acquire authentication token. Provide the token in the request `Authorization` header as `Bearer`.

### Request
To modify an venue information via PATCH method, provide the following venue details in the request:


```typescript
   {
    type: string
    name: string
    capacity: number
    bookingTerms: {
        fee: number
        timeSpan: string
    }
    availabilityStatus: string
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
}
```

**Notes**
- Booking timespan can only be `hour`, `day`, `week` or `month`.
- Availability status can only be `available`, `booked`, or `inactive`.

**Example:**

  ```javascript
   const data = {
        type: "5 star Hotel",
        name: "Paradise Eden",
        capacity: 20000,
        bookingTerms: {
            fee: 5000,
            timeSpan: 'day',
        },
        availabilityStatus: 'available',
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

1. PATCH Request Without venue pictures

```javascript

(async() => {
    const data = {`/data object above/`}

    const response = await fetch('<BASE_URL>/venues', {
        method: 'PATCH',
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

2. PATCH Request with an image File

```javascript

(async() => {
    const formData = {`FormData Object with venue pictures attached`}

    const response = await fetch('<BASE_URL>/venues', {
        method: 'PATCH',
        body: formData,
        headers:{
            'Authorization': 'Bearer <token>'
        }
    })

    const body = await response.json()

    console.log('venue: ', body)
})()
```

### Response

A successful response from this endpoint has the status code of `200`. The URL of the created item is in the `Location` header of the response object in the format `/venues/<venue._id`>. The response body contains updated venue document. The following is an example of a JSON payload returned in the response body.

```json

```

If the document to be updated does not exist, a response with status code of `404` is sent.
