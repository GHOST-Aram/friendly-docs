## PUT `users/:id`

This endpoint allows you to modify the details of a specific user.

### Authenticated

Only authenticated users can update their information. A user can only update a document they own. If a user tries to update a document owned by another user, a `Forbidden` response with status code `403` will be sent. 

Visit the [authorization documentation](../../../authentication/authentication.md) to learn how to acquire an authentication token.


### Request

Provide the ID of the user as a URL parameter. The ID in the parameter has to be the same as the ID of the user sending this request, this is because users can only update their own details and not the details of other users.

Provide any or all of the following user details in the request body to modify a user document:

```typescript
    profilePicture?: File 
    pictureUrl?: string
    fullName: string
    email: string
    password: string 
    userGroup?: 'host' | 'organizer' | 'attendee' | 'superuser'
```

Provide the *authorization token* as Bearer in the `Authorization` header of the request.

**Notes:**
- The `userGroup` can only be a `host`, `organizer`, an `attendee`, or a `superuser`. If not provided, the system will use the `attendee` group as default. 

- The users of the `host` group are the owners/managers/landlords of event venues.
- The users of the group `organizer` are event organizers.
- The users of the group `attendee` are prospective attendees of an event.
- The `superuser` group is reserved for system admins only.

- The profile picture is optional but if provided, must be an image file with the extension *.jpg, .jpeg, .png, .avif, or .jfif*
- Password can be any string of length between 8 and 100 characters

**Example:**

1. With Profile picture

```javascript
(async() =>{
    const formData = new FormData()

    formData.append('fullName', 'Curtis Jackson')
    formData.append('email', 'Nyasia.Kreiger@gmail.com')
    formData.append('profilePicture', '<variable holding a selected file>')
    
    
    const response = await fetch('<BASE_URL>/users', {
        method: 'PATCH',
        body: formData,
        headers: {
            'Authorization': 'Bearer <authToken>'
 }
 })

    const body = await response.json()

    console.log('User: ', body)
})()
```

2. Without Profile picture:

```javascript
(async() =>{

    const data = {
        fullName: 'Curtis Jackson'
        email: 'Nyasia.Kreiger@gmail.com'
 }
    
    
    const response = await fetch('<BASE_URL>/users', {
        method: 'PATCH',
        body: JSON.stringify(data),
        headers:{
            'Content-Type': 'application/json',
            'Authorization': 'Bearer <authToken>'
 }
 })

    const body = await response.json()

    console.log('User: ', body)
})()
```

### Response

A successful response from this endpoint has a status code of `200`.  The URL to the updated user documents is available in the `Location` header of the response object. The response body contains a json payload containing the updated user details. Below is an example of a user document returned in the response body.


```json
{
    "_id": "66aa425d6e3b901410065476",
    "fullName": "Darlene Hills",
    "userGroup": "superuser",
    "email": "RafaelBergnaum@yahoo.com",
    "__v": 0
}
```

If the document to be modified is not, a response with a status code of `404` is sent.