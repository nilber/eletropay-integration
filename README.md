**EletroPay Integration**
----
  
  
We need your application to have a private API (for security reasons we recommend that only EletroPay should have access to this environment) with the following requirements.

  ## Your API
  
  ### Register
We need to register the eletropay user on your system, a way to associate the POS with your company.

**URL** : `"/v1/clients"`

**Method** : `POST`

**Data constraints**

```json
{
    "email": "[valid email address]"
}
```

**Data example**

```json
{
    "email": "ep@example.com"
}
```

## Success Response

**Code** : `200 OK`

**Content example**

```json
{
    "token": "93144b288eb1fdccbe46d6fc0f241a51766ecd3d"
}
```

Let's use this token for all requests to get addresses.




  ### Get New Address
Method for obtaining an address on your platform.

**URL** : `"/v1/clients/:token/:currency"`

**Method** : `GET`

**Data constraints**

| Parameter | Description |
| --- | --- |
| token | Your client's token |
| currency | Cryptocurrency Initials You Want to Obtain an Address |

**Data example**

| Parameter | Description |
| --- | --- |
| token | 93144b288eb1fdccbe46d6fc0f241a51766ecd3d |
| currency | DASH |

## Success Response

**Code** : `200 OK`

**Content example**

```json
{
    "address": "Xc5DnvSCAuB9PXU7p35Sp6FCAPHU7Ge6Cr"
}
```

This address will be forwarded to POS.




  ### Callback when detecting a payment
Use this function to notify the POS that the payment has been successfully detected.
This endpoint will be informed by EletroPay, below the example request that should be executed.

**URL** : `"/v1/payments/:key/:currency/"`

**Method** : `POST`

**Data constraints**

```json
{
  "amount": [transfer amount],
  "confirmations": [amount of confirmations],
  "address":"[transaction address]",
  "txid": "[transaction identifier, recommended to use txid obtained from blockchain for transaction]"
}
```

**Data example**

```json
{
  "amount": 0.00028443,
  "confirmations": 5,
  "address":"Xc5DnvSCAuB9PXU7p35Sp6FCAPHU7Ge6Cr",
  "txid": "f23f2dfb3c842fe025c9127f26c51482e7565fd180d8e84fe803cdd4baed869"
}
```

## Success Response

**Code** : `200 OK`

**Content example**

```json
OK
```

You can update the commits field and make further use of this API when you reach the required amount of commits on your platform.
