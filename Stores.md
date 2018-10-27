## List of methods:  
### Get all the stores of a business.  
`.getAllStores()` - Returns all the stores.  

### Get nearest deliverable store with respect to a lat/lng.
`.getStore(params)` 
Params:  
```
{
   lat:<Latitude>,
   lng:<Longitude>
}
```
This will throw an error if lat/lng is not provided.  
This will return `success:false` in the following case:  
1) No store found.  
2) Store found but temporarily closed.  
3) Store found but closed for the day.  
NOTE: `error_message` has to be configured in CRM.


## [NEXT - Checkout session](https://github.com/urbanpiper/up-sdk/wiki/Checkout)