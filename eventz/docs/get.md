## GET `/events`

This endpoint allows the client to retrieve a list of events. The endpoint responds with a paginated list by default. The default pagination limit is 10. You can change this value using query parameters.


## Authorization
All users, including anonymous users, can view event listings. Authentication is therefore not required for this endpoint.

### Request
You can send a request to fetch a list of events with the desired pagination constraints. Pagination constraints can be defined using the following query parameters:

- `page`: number
- `limit`: number

Pagination constraints can be included in the URL as shown in the following URL

```t
/events?page=2&&limit=21
```

If the request does not include client-defined pagination constraints, the system will use its default pagination constraints to process the request.

You can also further refine your search by using query parameters. The following is a list of parameters that you can include in the query string:

- `category`, 
- `venue`, 
- `title`, 
- `createdBy`- The Id of the user who posted the event, 
- `city`

**Example**

```javascript
(async() =>{

    const response = await fetch('<BASE_URL>/events?page=2&&limit=21', {
        method: 'GET',
 })

    const body = await response.json()

    console.log('events: ', body)
})()
 ```

### Response
A successful response from this endpoint has a status code of `200`. The list of events is in the response body as a JSON payload. The following is an example of the JSON payload in the response body:

```json
[
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
]
```