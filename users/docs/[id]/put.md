## PUT `users/:id`

This endpoint allows you to apply full updates on the details of a specific user.

### Authenticated

Only authenticated users can update their information. Visit the [authorization documentation](../../../authentication/authentication.md) to learn how to acquire authentication token.


### Request

Provide the id of the user as a url parameter. The id in the parameter has to be the same as the id of the user sending this request, this is because users can only update their own details and not the details of other users.

Provide the authorization token as Bearer in the `Authorization` header of the request.

To update information for a specific user, provide the following user details in the request body:

```typescript
    profilePicture?: File 
    pictureUrl?: string
    fullName: string
    email: string
    password: string 
    userGroup?: 'organizer' | 'attendee' | 'superuser'
```

**Notes:**
- The `userGroup` can only be an `organizer`, an `attendee` or a `superuser`. If not provided, the system will use the `attendee` group as default.
- The `superuser` group is reserved for system admins only.
- The profile picture is optional but if provided, must be an image file with the extension * .jpg, .jpeg, .png , .avif, and .jfif*
- Password can be any string of length between 8 and 100 characters

### Response

A successfull PUT request receives a response with a status code of 200. If the document to be updated does not exist, a new document is created and a response with status code of 201 is sent. 

The URL to the updated user documents is available in the `Location` header of the response object. The response body contains a json payload containing the updated user details.

### Example:

1. With Profile picture

```javascript
(async() =>{
    const formData = new FormData()

    formData.append('fullName', 'Curtis Jackson')
    formData.append('email', 'Nyasia.Kreiger@gmail.com')
    formData.append('password', 'password3')
    formData.append('userGroup', 'host')
    formData.append('profilePicture', '<variable holding a selected file>')
    
    
    const response = await fetch('<BASE_URL>/users', {
        method: 'PUT',
        body: formData
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
        password: 'password3'
        userGroup: 'organizer'
    }
    
    
    const response = await fetch('<BASE_URL>/users', {
        method: 'PUT',
        body: JSON.stringify(data),
        headers:{
            'Content-Type': 'application/json'
        }
    })

    const body = await response.json()

    console.log('User: ', body)
})()
```