# Javascript SDK for UP

## Basic Setup  
The UP SDK for JavaScript doesn't have any standalone files that need to be downloaded or installed, instead, you simply need to include a short piece of regular JavaScript in your HTML that will asynchronously load the SDK into your pages. The async load means that it does not block loading other elements of your page.
You should insert the following snippet of code it directly after the opening `body` tag on each page you want to load it.

```
window.UPAsyncInit = ()=>{
  UP_SDK.init({
    apiKey:<api_key>,
    …..
  })
}

 
(function(d){
        var js, id = 'up-jssdk', ref = d.getElementsByTagName('script')[0];
        if (d.getElementById(id)) {return;}
        js = d.createElement('script'); js.id = id; js.async = true;
        js.src = "https://test-sdk.urbanpiper.com/";
        js.onload = UPAsyncInit;
        ref.parentNode.insertBefore(js, ref);
}(document));
```

# Init  
> Initialize and setup the SDK. All other SDK methods must be called after this one.  
> `init` is a *synchronus* call and it returns certain persistent information that might be required later.  
> Any sdk method should be called after init call.
  
Reqiured params:  
```
{
  "API_KEY": "bb30b3e53176f7b249bf0b16652a5afd0dc5f9de",
  "USERNAME": "biz_tst_vjUSsDcewHRIZCFjCARVZn",
  "ENV": <staging|production>,
  "LANG": "en"
}
```  
All functions are promised based. Can be used as:  
`let resp = await UP_SDK.login(params)`  
or  
`UP_SDK.login(params).then((resp)=>{}).catch((err)=>{})`

# Response structure  
Response for all methods is:    
```
{
   success: <true|false>,
   data: {    
   },
   error_message: "error message"
}
```

### Available methods for modules:  
1. [Authentication](https://github.com/urbanpiper/up-sdk/wiki/Authentication)  
2. [Stores](https://github.com/urbanpiper/up-sdk/wiki/Stores)  
3. [Checkout](https://github.com/urbanpiper/up-sdk/wiki/Checkout)  
|------ [Catalogue](https://github.com/urbanpiper/up-sdk/wiki/Catalogue)  
|------ [Cart](https://github.com/urbanpiper/up-sdk/wiki/Cart)  
|------ [Order](https://github.com/urbanpiper/up-sdk/wiki/Order)  
