## GET /users

This endpoint allows the client to retrieve a list of users that are registered with the system. 

The response returns a paginated list by default, the default pagination limit is 10, you can change this value using query parameters.


## Authorization
Only authenticated users with admin rights (superusers) can read the list of all users. Visit the [authentication documentation](../authentication/auth.md) to find out how to get authorization token.

### Request
You can send a request to view list of users with the desired pagination constraints or without pagination constraints. If the request does not include client defined constraints, the system will use it's default pagination constraints to process the request. Pagination constraints can be defined using the following query parameters:

- `page`: number
- `limit`: number

Pagination constraints can be included in the url as shown in the following URL

```t
/users?page=2&&limit=21
```


### Response
A success response from this endpoint has a status code of 200. The list of users is contained in the response body as a JSON payload. Each object in the users array contains the following user details:

```javascript
    _id: string
    fullName: String
    email: string
    password: string
    userGroup: string
    pictureUrl?: string
    profilePicture: {
        data: string 
        name: string 
        contentType: string 
    }
```

**Notes**
- The `_id` is a unique 24 character hexadecimal string
- The profile picture in the response is formated into a base64 data string that can be converted into a file using browser APIs. 
- The picture profile name represents the original name of the file. 
- The content type represent the files mimetype


## Example

```javascript
(asyn() =>{

    const response = await fetch('<BASE_URL>/users', {
        method: 'GET',
        headers: {
            'Authorization': 'Bearer<token>'
        }
    })

    const body = await response.json()

    console.log('Users: ', body)
})()
 ```