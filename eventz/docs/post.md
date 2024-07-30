## POST `/events`

This endpoint allows event organizers to create a new event document.

### Authorization
Only authenticated event organizers can create events. Event organizers are users of the `organizer` user group. Visit the [authentication docs](../authentication/authentication.md) to acquire authentication token. Provide the token in the request `Authorization` header as `Bearer`.

### Request
To create a new event, provide the following event details in the request body:

```typescript
    category: string
    graphic: File
    venue: string
    title: string
    city: string
    date: string
    time: {
        start: string
        end?: string
        zone: string
    }
    duration: string
    ageLimit: {
        min: number,
        max: number
    }
    availableTickets: number
    ticketPrice: number
```


**Notes**
- The event graphic is optional but if provided, must be an image file with the extension *.jpg, .jpeg, .png , .avif, or .jfif*
- The accepted value of the `date` string is in the format *Day MonthName Year*. For example *12 January 2025*.
- The accepted values of `time.start` and `time.end` strings are in the format *hour:minutes AM or PM*.
- The value of `time.end` is optional.
- The accepted value of `time.zone` string is in the format *GMT+hours:minutes*. For example *GMT+03:00*.
- The accepted value of `duration` string is in the format *Number days or hours or minutes*. For example *3 days or 3 hours or 45 minutes*.

**Example:**

  ```javascript
    const data = {
        category: "Music Concert",
        venue: "Quiver Lounge",
        title:"Ramogi Night",
        city: "Nairobi",
        date: "23 July 2024",
        time: {
            start: "12:37 PM",
            end: "03:37 PM",
            zone: "GMT+03:00"
        },
        duration: "3 days",
        ageLimit: {
            min: 17,
            max: 25
        },
        availableTickets: 100,
        ticketPrice: 2500
    }
```

1. POST Request Without an Image File

```javascript

(async() => {
    const data = {`/data object above/`}

    const response = await fetch('<BASE_URL>/events', {
        method: 'POST',
        body: JSON.stringify(data),
        headers:{
            'Content-Type': 'application/json',
            'Authorization': 'Bearer <token>'
        }
    })

    const body = await response.json()

    console.log('event: ', body)
})()
```

2. POST Request with an image File

```javascript

(async() => {
    const formData = {`FormData Object with an image file attached`}

    const response = await fetch('<BASE_URL>/events', {
        method: 'POST',
        body: formData,
        headers:{
            'Authorization': 'Bearer <token>'
        }
    })

    const body = await response.json()

    console.log('event: ', body)
})()
```

### Response

A successful response from this endpoint has the status code of `201`. The response body contains the created event document. The URL of the created item is in the `Location` header of the response object in the format `/events/<event._id`>.
