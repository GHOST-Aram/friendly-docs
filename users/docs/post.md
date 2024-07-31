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
    userGroup?: 'host'|'organizer' | 'attendee' | 'superuser'
```

**Notes:**
- The `userGroup` can only be a `host`, `organizer`, an `attendee` or a `superuser`. If not provided, the system will use the `attendee` group as default. 

- The users of the `host` group are the owners/managers/landlords of event venues.
- The users of the group `organizer` are event organizers.
- The users of the group `attendee` are prospective attendees of an event.
- The `superuser` group is reserved for system admins only.

- The profile picture is optional but if provided, must be an image file with the extension *.jpg, .jpeg, .png , .avif, or .jfif*
- Password can be any string of length between 8 and 100 characters

**Examples:**

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
### Response

A successful response from this endpoint has the status code of `201`. The response body contains created user document. The URL of the created item is in the `Location` header of the response object in the format `/users/<user_id`>. You can rely on this URL to view user profile after creating a new user. 

Below is an example of user document returned in the response body.

```json
{
    "_id": "669e526fa9ed3824e6db2db9",
    "fullName": "Darlene Hills",
    "userGroup": "superuser",
    "email": "RafaelBergnaum@yahoo.com",
    "password": "$2b$10$NkE10T4T8zCVvIawiFHkb.MRV19Nstb9do.aD58pGAaq.um1aPa4i",
    "__v": 0
}
```