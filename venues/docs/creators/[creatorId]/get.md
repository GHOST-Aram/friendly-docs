## GET `/venues/creators/:creatorId`

This endpoint allows the client to retrieve a list of venues created by a specific venue host. 

The response returns a paginated list by default. The default pagination limit is 10. You can change this value using query parameters.


## Authorization
All users, including anonymous users, can view venues listed by specific host. Authentication is therefore not required for this endpoint.

### Request
You can send a request to view list of venues with the desired pagination constraints.  Pagination constraints can be defined using the following query parameters:

- `page`: number
- `limit`: number

Pagination constraints can be included in the url as shown in the following URL

```t
/venues/creators/<creatorId>?page=2&&limit=21
```

If the request does not include client defined pagination constraints, the system will use it's default pagination constraints to process the request.

**Example**

```javascript
(asyn() =>{

    const response = await fetch('<BASE_URL>/venues/creators/<creatorId>?page=2&&limit=21', { method: 'GET' })

    const body = await response.json()

    console.log('venues: ', body)
})()
 ```

### Response
A success response from this endpoint has a status code of `200`. The list of venues is contained in the response body as a JSON payload. The following is an example of data returned in the response body:
