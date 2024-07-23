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
- Password can be any string of length between 8 and 100 characters
- The `userGroup` can only be a `organizer`, an `attendee` or a `superuser`. If not provided, the system will use the `attendee` group as default.
- Users can set profile pictures from file uploads but this will only be allowed in `PATCH` updates.

### Response

A successful response from this endpoint has the status code of `201`. The response body contains created user document. The URL of the created item is in the `Location` header of the response object in the format `/users/<user_id`>. You can rely on this URL to view user profile after creating a new user.


Example:

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