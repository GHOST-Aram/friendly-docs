## GET `/venue-types`

This endpoint allows the client to retrieve a list of venue types. 

The response returns a paginated list by default. The default pagination limit is 10. You can change this value using query parameters.


## Authorization
All users, including anonymous users, can view venue types listings. Authentication is therefore not required for this endpoint.

### Request
You can send a request to fetch a list of venue types with the desired pagination constraints. Pagination constraints can be defined using the following query parameters:

- `page`: number
- `limit`: number

Pagination constraints can be included in the URL as shown in the following URL

```t
/venue-types?page=2&&limit=21
```

If the request does not include client-defined pagination constraints, the system will use its default pagination constraints to process the request.

**Example**

```javascript
(async() =>{

    const response = await fetch('<BASE_URL>/venue-types?page=2&&limit=21', {
        method: 'GET',
 })

    const body = await response.json()

    console.log('venues types: ', body)
})()
 ```

### Response
A successful response from this endpoint has a status code of `200`. The list of venues is contained in the response body as a JSON payload. The following is an example of the JSON payload contained in the response body:

```json
[
 {
        "_id": "66ab81ff64f0899f1d8a3980",
        "name": "Sports Center or Stadium",
        "description": "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Maiores libero illo praesentium autem nesciunt consectetur repudiandae omnis eum similique in, quas rerum. Eveniet, possimus doloremque?",
        "createdBy": "66aa43ae6e3b901410065479",
        "__v": 0
 },
 {
        "_id": "66ab829b64f0899f1d8a3983",
        "name": "Sports Center or Stadium",
        "description": "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Maiores libero illo praesentium autem nesciunt consectetur repudiandae omnis eum similique in, quas rerum. Eveniet, possimus doloremque?",
        "createdBy": "66aa43ae6e3b901410065479",
        "__v": 0
 }
]
```