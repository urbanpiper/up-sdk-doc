To use cart methods, `checkoutSession` object is required. Can be created by `let c = UP_SDK.checkoutSession(params)`
[Read more about checkout session](https://github.com/urbanpiper/up-sdk/wiki/Checkout)

## Add to cart:  
`c.addToCart(itemObj, qty)` - this takes `itemObj` as first argument and `qty` as second argument (opptional). Default value of `qty` is 1;
`itemObj` has to be a valid item obj.  

## Remove from cart:  
`c.removeFromCart(id, qty)` - this takes `id` as first argument and `qty` as second argument (opptional). Default value of `qty` is 1;


## Get cart obj:  
`c.getCart()` - this will return cart object with related informations.  
i.e.
```
{
    "success": true,
    "data": {
        "items": [
            {
                "id": 123,
                "name": "dummy item",
                "quantity": 4,
                "price": 250 
            }
        ],
        "total": 250
    }
}
```

## [NEXT - Process order](https://github.com/urbanpiper/up-sdk/wiki/Order)