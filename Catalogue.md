Make sure, there is an active checkout session. [Read more](https://github.com/urbanpiper/up-sdk/wiki/Checkout/)

`let c = UP_SDK.checkoutSession(params)`  

## Get category  
`c.getAllCategories()` - will return all categories.  
`c.getStoreCategories()` - will return all categories of the store.  
Read more about [Stores](https://github.com/urbanpiper/up-sdk/wiki/Stores/)  
_NOTE: The response can be in-memory cached._

## Get Items  
`c.getItems({category_id})` - will return all the items of the category having id `category_id`.  

## Get item details  
`c.getItemDetails({item_id})` - will return items detail of the item having id `item_id`.  

## [NEXT - Cart related methods](https://github.com/urbanpiper/up-sdk/wiki/Cart)