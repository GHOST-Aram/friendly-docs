## GET `events/:id`

This endpoint allows the client to retrieve the details of an event using a specified event ID.

### Authorization
All users, including anonymous users, can view event details. Authentication is therefore not required for this endpoint.

### Request
Provide the event id as a url parameter in the url as shown below to fetch the details of an event:

```javascript
/events/<eventId>
```

**Example**

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
A successful response sent from this endpoint has a status code of `200`. The response body contains the event details as a JSON payload. The following is an example of the JSON payload contained in the response body:

```json

```

If the event document with the provided Id is not found, a response with status code `404` is sent.