## Place order
Placing order involves two steps:  
Note: You should have an active checkout session. [Read more about checkout session](https://github.com/urbanpiper/up-sdk/wiki/Checkout)

### 1) Preprocess the order to create a bill.
`c.makeBill()` - This creates a bill object.

**Important:** The bill object will contain the available payment options for that specific order. User should not be allowed to select any other payment option while placing an order.

However, this values can be overridden by passing the obj in `.makeBill`.   
`c.makeBill` will always have to be called before calling placing order.  
`c.makeBill` will return the bill which includes all required information that can be shown in UI.  

NOTE: Any charges, total, taxes should not be calculated client side. Information will be available in the response of `c.makeBill`. Or the last generated bill can be accessed by calling `.getBill`  

### 2) Place order:  
`c.placeOrder(params)`  
Params:
```
{
    phone: <phone no>,
    payment_option: <cash | wallet>,
    delivery_datetime: <timestamp>,
    instructions: <instructions>
}
```  
On success, ideally `c.destroyCart` should be called.

_NOTE: `c` is active checkout instance_