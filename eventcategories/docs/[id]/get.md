## GET `event-categories/:id`

This endpoint allows users to retrieve details of an Event Category using a specified Event Category ID.

### Authorization
All users, including anonymous users, can view details of an Event Category. Authentication is therefore not required for this endpoint.


### Request
To get the details of a Event Category with a specific id, provide the id as a url parameter in the request url as shown below:

```javascript
'/event-categories/<eventCategory._id>'
```

#### Example

```javascript
(async() =>{
    const response =  await fetch('<BASE_URL>/event-categories/65e40da5c390b114451cebb5',{
        method: 'GET',
    })

    const body = await response.json()
    console.log(body)
})()
```

### Response
A successful response sent from this endpoint has a status code of 200. The details are contained in the response body as a json payload. The JSON payload contains a Event Category object with the following details:

```javascript
    _id: string
    name: string
    description: string
    createdBy?: ObjectId
    graphic?: {
        name: string,
        data: string
        contentType: string
    }
```
