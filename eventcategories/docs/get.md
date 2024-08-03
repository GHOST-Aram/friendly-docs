## GET `/event-categories`

This endpoint allows the clients to retrieve a list of Event Categories. The response returns a paginated list by default. The default pagination limit is 10. You can change this value using query parameters.


## Authorization
All users, including anonymous users, can view event listings. Authentication is therefore not required for this endpoint.

### Request
You can send a request to fetch the list of event categories with customized pagination constraints. Pagination constraints can be defined using the following query parameters:

- `page`: number
- `limit`: number

Pagination constraints can be included in the URL as shown in the following URL

```javascript
'/event-categories?page=2&&limit=21'
```

If the request does not include client-defined pagination constraints, the system will use its default pagination constraints to process the request.

**Example**

```javascript
(async() =>{

    const response = await fetch('<BASE_URL>/event-categories?page=2&&limit=21', {
        method: 'GET',
 })

    const body = await response.json()

    console.log('Event Categories: ', body)
})()
 ```

### Response
A successful response from this endpoint has a status code of `200`. The response body contains the list of event categories as a JSON payload. The following is an example of the JSON payload contained in the response body:

```json
[
 {
        "_id": "66ab96e41b17e9888286df55",
        "name": "Lorem Ipsum Sudus",
        "description": "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Maiores libero illo praesentium autem nesciunt consectetur repudiandae omnis eum similique in, quas rerum. Eveniet, possimus doloremque?",
        "createdBy": "66aa441b6e3b90141006547c",
        "__v": 0
 },
 {
        "graphic": {
            "name": "1722521452423_drag-drop.png",
            "data": "iVBORw0KGgoAAAANSUhEUgAAAl0AAAE0CA...",
               "contentType": "image/png"
 },
        "_id": "66ab976c1b17e9888286df57",
        "name": "Lorem ipsum suudus",
        "description": "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Maiores libero illo praesentium autem nesciunt consectetur repudiandae omnis eum similique in, quas rerum. Eveniet, possimus doloremque?",
        "createdBy": "66aa441b6e3b90141006547c",
        "__v": 0
 }
]
```
