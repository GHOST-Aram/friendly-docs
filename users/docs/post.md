## POST `/users`

This endpoint allows you to create a new user.

### Authorization
You do not need authorization to use this endpoint.

### Request
provide the following user details in the request body to create a new user:

```typescript
    pictureUrl?: string
    fullName: string
    email: string
    password: string 
    profilePicture: File
    userGroup?: 'host'|'organizer' | 'attendee' | 'superuser'
```

**Notes:**
- The `userGroup` can only be a `host`, `organizer`, an `attendee`, or a `superuser`. If not provided, the system will use the `attendee` group as default. 

- The users of the `host` group are the owners/managers/landlords of event venues.
- The users of the group `organizer` are event organizers.
- The users of the group `attendee` are prospective attendees of an event.
- The `superuser` group is reserved for system admins only.

- The profile picture is optional but if provided, must be an image file with the extension *.jpg, .jpeg, .png, .avif, or .jfif*
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

A successful response from this endpoint has the status code of `201`. The URL of the created item is in the `Location` header of the response object in the format `/users/<user_id`>. The response body contains the created user document. Below is an example of a user document returned in the response body:

```json
// without file

{
    "fullName": "Frank Odoi",
    "pictureUrl": "https://cloud.mongodb.com/v2/64ae67d7c53a03549c2f2fad#/metrics/replicaSet/64ae67fef45c296f5e5c64f8/explorer/vestiger-users/users/find",
    "userGroup": "superuser",
    "email": "frankodoi9@gmail.com",
    "_id": "66aa594b8b3a69985f9862f0",
    "__v": 0
}

// with File
{
    "fullName": "Frank Odoi",
    "profilePicture": {
        "data": "/9j/4ddIRXhpZ...",
        "name": "1722439413210_20240318_165915.jpg",
        "contentType": "image/jpeg"
 },
    "userGroup": "superuser",
    "email": "frankodoi77@gmail.com",
    "_id": "66aa56f5065be438fdd14b4e",
    "__v": 0
}
```