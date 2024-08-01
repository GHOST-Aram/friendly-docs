## GET `venues/:id`

This endpoint allows you to retrieve the details of a venue using a specified venue ID.

### Authorization
All users, including anonymous users, can view venue details. Authentication is therefore not required for this endpoint.

### Request
Provide the id of the event document to be fetched as a url parameter in the url as shown below:

```javascript
'/venues/<venueId>'
```

**Example**

```javascript
(async() =>{
    const response =  await fetch('<BASE_URL>/venues/66aa9be5e641b3d6e3c020d3',{
        method: 'GET',
    })

    const body = await response.json()
    console.log(body)
})()
```

### Response
A successful response sent from this endpoint has a status code of `200`. The venue details are contaied in the response body as a JSON payload. The following is an example of a JSON payload contained in the response body:

```json
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

If a document with the requested Id is not found, a response of status `404` is returned.