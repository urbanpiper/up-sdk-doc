## Start with a checkout session  

Create a checkout session:
`let c = UP_SDK.checkoutSession(params)`  
Params (opptional):  
```
{
  fullfilmentmode:<delivery|pickup>
}
```
_NOTE: Default fullfilment mode is `delivery`._  
You can update the value anytime by calling `c.update(params)`  

## Set a store in your checkout session:  
`.setStore(storeObj)` - Read more about [Stores](https://github.com/urbanpiper/up-sdk/wiki/Stores/)  
`.getSelectedStore()` - will return selected store.  

Complete checkout process is described in 3 pages:  
* [Catalogue](https://github.com/urbanpiper/up-sdk/wiki/Catalogue)  
* [Cart](https://github.com/urbanpiper/up-sdk/wiki/Cart)  
* [Order process](https://github.com/urbanpiper/up-sdk/wiki/Order)  
