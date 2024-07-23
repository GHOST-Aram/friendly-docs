## GET `events/:id`

This endpoint allows you to retrieve event details using a specified event ID.

### Authorization
All users, including anonymous users, can view event details. Authentication is therefore not required for this endpoint.


### Request
To get the details of a event with a specific id, provide the id as a url parameter in the request url as shown below:

```javascript
/events/<eventId>
```

#### Example

```javascript
(async() =>{
    const response =  await fetch('<BASE_URL>/events/65e40da5c390b114451cebb5',{
        method: 'GET',
    })

    const body = await response.json()
    console.log(body)
})()
```

### Response
A successful response sent from this endpoint has a status code of 200. The event details are contaied in the response body as a json payload. The json payload contains a event object with the following details:

```javascript
    _id: string
   category: string
    venue: string
    title: string
    organizer: string,
    graphic: {
        name: string,
        data: string,
        contentType: string
    }
    city: string
    date: string
    time: {
        start: string
        end: string
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
