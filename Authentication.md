## Types of authentication:    
1) [Phone Authentication](#phone-authentication)
2) [Social Authentication](#social-authentication)  

# Phone Authentication    
### .login(params)  
> Log in user with phone number and password.  

Params:  
```
{
  phone:"+919833010430",
  password:"123456"
}
```  
### .logout()  
> Log out user. It will remove auth related information from localStorage.  

### .loginStatus()  
> This method is to check whether any auth info is present in the localStorage. the `success:true` doesn't garuntee the validity of the authHeader that is present in the response (If the user is logged in)

### .createUser(params)  
> Create new user.  

Params (Phone and password is required):  
```
{
  phone:"+919833010430",
  password:"123456",
  email:"mukesh@urbanpiper.com",
  name:"Mukesh"
}
```
### .verifyPhoneno(params)  
> After creating user, the user needs to verify the phone no.  

Required params:  
```
{
  phone:"+919833010430",
  pin:"12345"
}
```
### .forgotPassword(params)  
> Generate token that will be used to reset password. 

Required params:  
```
{
  phone:"+919833010430"
}
```
### .resetPassword(params)  
> To reset password with token. 

Required params:  
```
{
  phone:"+919833010430",
  pin:"1234", 
  new_password1:"12312", 
  new_password2:"12312"
}
```

# Social Authentication  
## Dependency:  
You have to get developer key and initialize FB and Google sdk separately.  
### Facebook:  
```
(function(d, s, id) {
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) return;
    js = d.createElement(s); js.id = id;
    js.src = "//connect.facebook.net/en_US/sdk.js";
    fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));

window.fbAsyncInit = function() {
    FB.init({
        appId      : <facbook-app-id>,
        cookie     : true,  // enable cookies to allow the server to access
        xfbml      : true,  // parse social plugins on this page
        version    : 'v2.8' // use graph api version 2.8
    });
}
```

### Google:  
```
var script = document.createElement("script");
script.src = "https://apis.google.com/js/platform.js?onload=googleSignInInit";
script.type = "text/javascript";
document.getElementsByTagName("head")[0].appendChild(script);

function googleSignInInit(){
    gapi.load('auth2', function(){
        // Retrieve the singleton for the GoogleAuth library and set up the client.
        window.auth2 = gapi.auth2.init({
            client_id: <google-client-id>,
            cookiepolicy: 'single_host_origin',
            // Request scopes in addition to 'profile' and 'email'
            scope: 'profile email'
        });
    });
}
```

Create social login instance for each provider: 
```
const socialLogin = UP_SDK.socialLogin({provider:<"facebook" | "google">})
```
Social login involves 3 steps:  
## Initiate social login  
> Call this method when user clicks on social login button. This method will use social `access_token` and check against UP server.   
```
socialLogin.init()
``` 
Response:  
```
{
  success: <true|false>,
  error_code: "phone_number_required"
  error_message: "Phone is required to verify"
}
```
There can be following cases:  
  1) Phone no required - When there is no record of the user in UP db.  
  2) Phone no is not verified - When the phone no associated with the account was not verified.  
  3) Failed to proceed - When the access token is spoofed.  
  4) Successful login.  

## Case1: Phone no is required.  
`error_code: phone_number_required`  
In this case, user should be asked to enter phone no. And call `socialLogin.checkPhone(params)`  
Params required:
```
{
  phone:"+919833010430"
}
```  
This method will send a verification code to phone no. On success, user should be asked to enter verification code. Call `socialLogin.register(params)`  
Params required:  
```
{
  pin:<verificationcode>
}
```
If `success:true`, registration is successful, you can also make subsequent API calls until you are calling `.logout()`.  

## Case 2: Phone no is not validated.  
`error_code: userbiz_phone_not_validated`  
In this state, user will have to go through "Forgot password flow."  

## Case 3: Access token is spoofed.  
`error_code: email_check_failed`  
Initiate the login again by calling `.init()`  

## Case 4: Successful login.  
If `success:true`, login is successful, you can also make subsequent API calls until you are calling `.logout()`.  

