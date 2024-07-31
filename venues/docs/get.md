## GET `/venues`

This endpoint allows the client to retrieve a list of venues. 

The response returns a paginated list by default. The default pagination limit is 10. You can change this value using query parameters.


## Authorization
All users, including anonymous users, can view venue listings. Authentication is therefore not required for this endpoint.

### Request
You can send a request to view list of venues with the desired pagination constraints.  Pagination constraints can be defined using the following query parameters:

- `page`: number
- `limit`: number

Pagination constraints can be included in the url as shown in the following URL

```t
/venues?page=2&&limit=21
```

If the request does not include client defined pagination constraints, the system will use it's default pagination constraints to process the request.

#### Example

```javascript
(asyn() =>{

    const response = await fetch('<BASE_URL>/venues?page=2&&limit=21', {
        method: 'GET',
    })

    const body = await response.json()

    console.log('venues: ', body)
})()
 ```

### Response
A success response from this endpoint has a status code of 200. The list of venues is contained in the response body as a JSON payload. Below is an example of the JSON payload returned in the response body:

```json
[
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
]
```