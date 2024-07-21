# The Authenticator

The Authenticator uses JWT tokens to control user access to various apps or parts of the apps in the system. The Authenticator does not register users. Users can be registered in a separate application disconnected from Authenticator. The app verifies the incoming user credentials against the credentials of registered users in the system before granting access. 

This app is only exposed on one route, a `POST` route. 

## POST `/auth`

If you provide correct credentials, you will receive response with status code `201` and an authorization token. For wrong credentials, you will receive an `Unauthorised` response with status code `401` and a reason for the response.

### Request
The endpoint accepts an a registered valid `email` andress and a `password` as input values. The password can be any string not be less than 8 characters and not longer than 100 characters.

``` json
{
    "email": "<registered user email>",
    "password": "< Correct user password>"
}

 ```

### Response

``` json
{
    "token": "<token>"
}
 ```
The code snippet below provides an example on how to make requests to this app.

```javascript
(async() =>{
    const body = JSON.stringify({
        email: "Curtis.Kreiger@gmail.com",
        password: "password43"
    })

    
    const response = await fetch('<BASE_URL>/auth', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body
    })

    const responseBody = await response.json()
    const status = response.status
    if(status === 201){
        console.log('Token: ', responseBody.token)
    } else{
        console.log("Status: ", status, "Body: ", responseBody)
    }
})()
```