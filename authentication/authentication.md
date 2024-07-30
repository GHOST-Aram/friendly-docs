# The Authenticator

The Authenticator uses JWT tokens to control user access to various apps or parts of the apps in the system. The Authenticator does not register users. Users can be registered in a separate application from Authenticator. The app verifies the user credentials stored in the authentication token against the credentials of registered users in the system before granting access. 

This app is only exposed on one route, a `POST` route. Below is a guide on how to acquire an authentication token through the `POST` route.

*POST  URL - `<BASE_URL>/auth`*


### Request
The endpoint accepts an a registered valid `email` andress and a `password` as input values. The password can be any string not be less than 8 characters and not longer than 100 characters.

``` json
{
    "email": "<registered user email>",
    "password": "< Correct user password>"
}

```

 The code snippet below provides an example on how to make requests to authenticator `POST` route.

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

### Response
If you provide correct credentials, you will receive response with status code `201` and an authorization token. The authorization token will be contained in the body of the response as a JSON string. For wrong credentials, you will receive a response with status code `401`, `Unauthorised`. 

The following code shows the structure of the content of the response body:

``` json
{
    "token": "<token>"
}
 ```