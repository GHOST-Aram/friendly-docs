## GET `event-categories/:id`

This endpoint allows users to retrieve details of an Event category by a specified event category ID.

### Authorization
All users, including anonymous users, can view details of an event category. Authentication is therefore not required for this endpoint.


### Request
Provide the id of the target event category as a url parameter as shown below to fetch its details:

```javascript
'/event-categories/<eventCategory._id>'
```

**Example**

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
A successful response sent from this endpoint has a status code of `200`. The details are contained in the response body as a JSON payload. The following is an example of the JSON payload contained in the response body:

```json
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
```

If the document with the provided Id is not found, a response with status code of `404` is returned.