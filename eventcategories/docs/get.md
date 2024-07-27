## GET `/event-categories`

This endpoint allows the clients to retrieve a list of Event Categories. 

The response returns a paginated list by default. The default pagination limit is 10. You can change this value using query parameters.


## Authorization
All users, including anonymous users, can view event listings. Authentication is therefore not required for this endpoint.

### Request
You can send a request to view list of Event Categories with customized pagination constraints. If the request does not include client defined pagination constraints, the system will use it's default pagination constraints to process the request. Pagination constraints can be defined using the following query parameters:

- `page`: number
- `limit`: number

Pagination constraints can be included in the url as shown in the following URL

```javascript
'/event-categories?page=2&&limit=21'
```

#### Example

```javascript
(asyn() =>{

    const response = await fetch('<BASE_URL>/event-categories?page=2&&limit=21', {
        method: 'GET',
    })

    const body = await response.json()

    console.log('Event Categories: ', body)
})()
 ```

### Response
A successfull response from this endpoint has a status code of `200`. The list of Event Categories is contained in the response body as a JSON payload. Each object in the Event Categories array contains the following event details:

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
