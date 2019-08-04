**EletroPay Integration**
----
  
  
We need your application to have a private API (for security reasons we recommend that only EletroPay should have access to this environment) with the following requirements.

  ## Your API
  
  ### Register
We need to register the eletropay user on your system, a way to associate the POS with your company.

**URL** : `"/v1/client"`

**Method** : `POST`

**Auth required** : Optional

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

**Auth required** : Optional

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

