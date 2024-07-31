## POST `/venues`

This endpoint allows venue hosts (venue managers/owners/landlords) to create a new venue. Venue hosts are users of the `host` user group

### Authorization
Only authenticated venue hosts can create venues. Visit the [authentication docs](../authentication/authentication.md) to acquire authentication token. Provide the token in the request `Authorization` header as `Bearer`.

### Request
To create a new venue, provide the following venue details in the request body:

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

1. POST Request Without an Image File

```javascript

(async() => {
    const data = {`/data object above/`}

    const response = await fetch('<BASE_URL>/venues', {
        method: 'POST',
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

2. POST Request with venue pictures

```javascript

(async() => {
    const formData = {`FormData Object with venue pictures attached`}

    const response = await fetch('<BASE_URL>/venues', {
        method: 'POST',
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

A successful response from this endpoint has the status code of `201`. The response body contains created venue document. The URL of the created item is in the `Location` header of the response object in the format `/venues/<venue._id`>. The following is an example of the data in the JSON payload:

```json
{

    //Without image files
    "type": "S star Hotel",
    "name": "Paradise Hole Mombasa",
    "capacity": 20000,
    "bookingTerms": {
        "fee": 500000,
        "timeSpan": "day"
    },
    "availabilityStatus": "available",
    "createdBy": "66aa43ae6e3b901410065479",
    "address": {
        "cityOrTown": "Nairobi",
        "street": "34 North",
        "block": {
            "name": "Paradise Hole Mombasa",
            "floor": 12
        }
    },
    "description": "Lorem ipsum dolor sit, amet consectetu adipisicing elit. Maiores libero illo praesentium autem nesciunt consectetur repudiandae omnis eum similique in, quas rerum. Eveniet, possimus doloremque?",
    "accessibilityFeatures": {
        "stairCase": true,
        "elevator": true,
        "escallator": false,
        "ramp": true
    },
    "coordinates": {
        "latitude": -36.3,
        "longitude": -12.5
    },
    "_id": "66aa959fa956d58c201e28db",
    "pictures": [],
    "__v": 0
}

//With image files
{
    "type": "5 start Hotel",
    "name": "Paradise Hotel Mombasa",
    "capacity": 20000,
    "bookingTerms": {
        "fee": 500000,
        "timeSpan": "day"
    },
    "availabilityStatus": "available",
    "createdBy": "66aa43ae6e3b901410065479",
    "address": {
        "block": {
            "name": "Paradise Hotle MSA",
            "floor": 12
        },
        "cityOrTown": "Mombasa",
        "street": "Ngina Drive"
    },
    "pictures": [
        {
            "name": "1722457061307_file-upload.png",
            "data": "iVBORw...",
            "contentType": "image/png",
            "_id": "66aa9be5e641b3d6e3c020d6"
        }
    ],
    "description": "Lorem ipsum dolor sit, amet consectetu adipisicing elit. Maiores libero illo praesentium autem nesciunt consectetur repudiandae omnis eum similique in, quas rerum. Eveniet, possimus doloremque?",
    "accessibilityFeatures": {
        "stairCase": true,
        "elevator": true,
        "escallator": false,
        "ramp": true
    },
    "coordinates": {
        "latitude": -36.3,
        "longitude": -12.5
    },
    "_id": "66aa9be5e641b3d6e3c020d3",
    "__v": 0
}
```
