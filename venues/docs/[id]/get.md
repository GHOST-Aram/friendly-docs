## GET `venues/:id`

This endpoint allows you to retrieve venue details using a specified venue ID.

### Authorization
All users, including anonymous users, can view venue details. Authentication is therefore not required for this endpoint.


### Request
To get the details of a venue with a specific id, provide the id as a url parameter in the request url as shown below:

```javascript
/venues/<venueId>
```

#### Example

```javascript
(async() =>{
    const response =  await fetch('<BASE_URL>/venues/65e40da5c390b114451cebb5',{
        method: 'GET',
    })

    const body = await response.json()
    console.log(body)
})()
```

### Response
A successful response sent from this endpoint has a status code of 200. The venue details are contaied in the response body as a json payload. The json payload contains a venue object with the following details:

```javascript
    {
    type: string
    name: string
    capacity: number
    host?: ObjectId
    address: {
        cityOrTown: string
        street: string
        block: {
            name: string,
            floor: number
        }
    }
    pictures?: {
        name: string
        data: Buffer
        contentType: string
    }[]
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
