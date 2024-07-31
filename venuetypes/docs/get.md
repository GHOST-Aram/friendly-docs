## GET `/venue-types`

This endpoint allows the client to retrieve a list of venue types. 

The response returns a paginated list by default. The default pagination limit is 10. You can change this value using query parameters.


## Authorization
All users, including anonymous users, can view venue types listings. Authentication is therefore not required for this endpoint.

### Request
You can send a request to fetch a list of venue types with the desired pagination constraints. Pagination constraints can be defined using the following query parameters:

- `page`: number
- `limit`: number

Pagination constraints can be included in the url as shown in the following URL

```t
/venue-types?page=2&&limit=21
```

If the request does not include client defined pagination constraints, the system will use it's default pagination constraints to process the request.

**Example**

```javascript
(asyn() =>{

    const response = await fetch('<BASE_URL>/venue-types?page=2&&limit=21', {
        method: 'GET',
    })

    const body = await response.json()

    console.log('venues types: ', body)
})()
 ```

### Response
A success response from this endpoint has a status code of `200`. The list of venues is contained in the response body as a JSON payload. The following is an example of the JSON payload contained in the response body:

```json

```
