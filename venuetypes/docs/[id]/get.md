## GET `venue-types/:id`

This endpoint allows users to retrieve venue types details using a specific venue type ID.

### Authorization
All users, including anonymous users, can view venue type details. Authentication is therefore not required for this endpoint.


### Request
To get the details of a venue type with a specific id, provide the id as a url parameter in the request url as shown below:

```javascript
/venue-type/<venueId>
```

#### Example

```javascript
(async() =>{
    const response =  await fetch('<BASE_URL>/venue-type/65e40da5c390b114451cebb5',{
        method: 'GET',
    })

    const body = await response.json()
    console.log(body)
})()
```

### Response
A successful response sent from this endpoint has a status code of `200`. The venue type details are contaied in the response body as a json payload. The json payload contains a venue object with the following details:

```javascript
    {
        _id: string
        name: string
        createdBy: ObjectId
        description: string
    }
```
