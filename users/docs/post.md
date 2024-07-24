## POST `/users`

This endpoint allows you to create a new user.

### Authorization
You do not need authorization to use this endpoint.

### Request
To create a new user, provide the following user details in the request body:

```typescript
    pictureUrl?: string
    fullName: string
    email: string
    password: string 
    userGroup?: 'organizer' | 'attendee' | 'superuser'
```

**Notes:**
- The `userGroup` can only be a `organizer`, an `attendee` or a `superuser`. If not provided, the system will use the `attendee` group as default. 
- The `superuser` group is reserved for system admins only.
- The profile picture is optional but if provided, must be an image file with the extension *.jpg, .jpeg, .png , .avif, or .jfif*
- Password can be any string of length between 8 and 100 characters


### Response

A successful response from this endpoint has the status code of `201`. The response body contains created user document. The URL of the created item is in the `Location` header of the response object in the format `/users/<user_id`>. You can rely on this URL to view user profile after creating a new user.


### Examples:

1. With Profile Picture:
```javascript
    (async() =>{
        const formData = new FormData()

        formData.append('fullName', 'Curtis Jackson')
        formData.append('email', 'Nyasia.Kreiger@gmail.com')
        formData.append('password', 'password3')
        formData.append('userGroup', 'host')
        formData.append('profilePicture', '<variable holding a selected file>')
        
        
        const response = await fetch('<BASE_URL>/users', {
            method: 'POST',
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
        method: 'POST',
        body: JSON.stringify(data),
        headers:{
            'Content-Type': 'application/json'
        }
    })

    const body = await response.json()

    console.log('User: ', body)
})()
```