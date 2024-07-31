## GET `/events/creators/:creatorId`

This endpoint allows the client to retrieve a list of events created by a specific event organizer. The endpoint responds with a paginated list by default. The default pagination limit is 10. You can change this value using request query parameters.

## Authorization
All users, including anonymous users, can view event listed by specific organizer. Authentication is therefore not required for this endpoint.

### Request
You can send a request to view list of events with the desired pagination constraints. Pagination constraints can be defined using the following query parameters:

- `page`: number
- `limit`: number

Pagination constraints can be included in the url as shown in the following URL

```t
/events/creators/<creatorId>?page=2&&limit=21
```

If the request does not include client defined pagination constraints, the system will use it's default pagination constraints to process the request.

**Example**

```javascript
(asyn() =>{

    const response = await fetch('<BASE_URL>/events/creators/<creatorId>?page=2&&limit=21', {
        method: 'GET',
    })

    const body = await response.json()

    console.log('events: ', body)
})()
 ```

### Response
A successfull response from this endpoint has a status code of `200`. The response body contains a list of event documents as a JSON payload. The following is an example of the JSON payload contained in the response body

```json

```
