## GET `events/:id`

This endpoint allows the client to retrieve the details of an event using a specified event ID.

### Authorization
All users, including anonymous users, can view event details. Authentication is therefore not required for this endpoint.

### Request
Provide the event ID as a URL parameter in the URL as shown below to fetch the details of an event:

```javascript
/events/<eventId>
```

**Example**

```javascript
(async() =>{
    const response =  await fetch('<BASE_URL>/events/65e40da5c390b114451cebb5',{
        method: 'GET',
 })

    const body = await response.json()
    console.log(body)
})()
```

### Response
A successful response sent from this endpoint has a status code of `200`. The response body contains the event details as a JSON payload. The following is an example of the JSON payload in the response body:

```json
 {
        "category": "Music",
        "venue": "Madison Square Garden",
        "title": "Rock Concert",
        "createdBy": "66aa441b6e3b90141006547c",
        "graphic": {
            "name": "1722444814279_20240318_165856.jpg",
            "data": "/9j/4dbgRXhpZgAASUkq...",
            "contentType": "image/jpeg"
 },
        "city": "Nairobi",
        "date": "8 August 2024",
        "time": {
            "start": "1300",
            "end": "2100",
            "zone": "GMT+03:00"
 },
        "duration": "8 hours",
        "ageLimit": {
            "min": 18,
            "max": 60
 },
        "availableTickets": 5000,
        "ticketPrice": 5900,
        "_id": "66aa6c0e1001f0abc83679d3",
        "__v": 0
 }
```

If the event document with the provided ID is not found, a response with the status code `404` is sent.