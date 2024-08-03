## GET `venue-types/:id`

This endpoint allows users to retrieve details of venue types using a specific venue type ID.

### Authorization
All users, including anonymous users, can view venue-type details. Authentication is therefore not required for this endpoint.


### Request
To get the details of a venue type with a specific ID, provide the ID as a URL parameter in the request URL as shown below:

```javascript
/venue-type/<venueId>
```

**Example**

```javascript
(async() =>{
    const response =  await fetch('<BASE_URL>/venue-type/65e40da5c390b114451cebb5',{
        method: 'GET',
 })

    const body = await response.json()
    console.log(body)
})()
```

### Response
A successful response sent from this endpoint has a status code of `200`. The venue type details in the response body as a json payload. The following is an example of the JSON payload in the response body:

```json
{
    "_id": "66ab81ff64f0899f1d8a3980",
    "name": "Sports Center or Stadium",
    "description": "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Maiores libero illo praesentium autem nesciunt consectetur repudiandae omnis eum similique in, quas rerum. Eveniet, possimus doloremque?",
    "createdBy": "66aa43ae6e3b901410065479",
    "__v": 0
}
```

If the document to be modified is not found, a response with a status code of `404` is sent.
