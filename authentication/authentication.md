# The Authenticator *POST  URL - `<BASE_URL>/auth`*

The Authenticator uses JWT tokens to control user access to various apps or parts of the apps in the system. The Authenticator does not register users. Users can be registered in a separate application from Authenticator. The app verifies the user credentials stored in the authentication token against the credentials of registered users in the system before granting access. 

This app is only exposed on one route, a `POST` route. Below is a guide on how to acquire an authentication token through the `POST` route.

### Request
The endpoint accepts a registered valid `email` address and a `password` as input values.

``` json
{
    "email": "<registered user email>",
    "password": "< Correct user password>"
}
```

**Note**
- The password can be any string not less than 8 characters and not longer than 100 characters

**Example**

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
You will receive a response with status code `201` if you provide the correct email and password. The response body contains the authorization token. The following is an example of the JSON payload contained in the response body:

``` json
 {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6IlJhZmFlbEJlcmduYXVtQGVyZC5lZHUiLCJmdWxsTmFtZSI6IkRhcmxlbmUgSGlsbHMiLCJ1c2VyR3JvdXAiOiJzdXBlcnVzZXIiLCJpZCI6IjY2YWE0MjVkNmUzYjkwMTQxMDA2NTQ3NiIsImlhdCI6MTcyMjQzNDE4MCwiZXhwIjoxNzI1MDI2MTgwLCJzdWIiOiI2NmFhNDI1ZDZlM2I5MDE0MTAwNjU0NzYifQ.ZIY4jzsg21IY2esNB9W5-XYU4p9_xbI_4LzyfqquNCI"
 }
 ```

If either the password or the email does not match, you will receive a response with status code `401`, `Unauthorised`. The response body will contain a text message showing which of the credentials did not match.