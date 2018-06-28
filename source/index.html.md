---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='http://fidely.com/'>Request Client Credentials</a>

  - <a href='https://github.com/lord/slate' class="slateInfo">Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the RedIN REST API! You can use our API to access Shops/Benefits API endpoints, which can get information on various shops/benefits, and filters in our database.

The javascript examples are made with axios. <a href="https://github.com/axios/axios"> axios docs </a>

More languages documentation coming soon.


# Authentication

> To retrieve the access_token, use this code:


```javascript
// Send a POST request
axios({
  method: 'post',
  url: 'https://fidely.auth0.com/oauth/token',
  data: {
    client_id: 'your_static_client_id',
    client_secret: 'your_static_client_secret',
    audience: 'https://api.redin.com.ar',
    grant_type: 'client_credentials'
  }
})
.then(function(response) {
  // save your access token contained in response
});
```

> Make sure to replace the variables `your_static_client_id` and `your_static_client_secret` with the values provided by us.


> The above scripts returns JSON structured like this:

```json
{
  "access_token": "eyJ0EXAMPLEeXAEXAMPLEQiLCJhbGcEXAMPLEI1NEXAMPLEpZCI6Ik1FUkdRakUzEXAMPLEqTTFORGN3TlVZNU56QTFOakF4TWpWR05UbEJOalF6TWpZeE5rVXpRZyJ9.eyJpc3MiOiJodHRwczovL2ZpZGVseS5hdXRoMC5jb20vIiwic3ViIjoiSUYxNU1USW9SeHcyRVVFTEpRZHRkTDA3SERRMFBGckpAY2xpZW50cyIsImF1ZCI6Imh0dHBzOi8vYXBpLnJlZGluLmNvbS5hciIsImlhdCI6MTUzMDExMjM4OCwiZXhwIjoxNTMwMTk4Nzg4LCJhenAiOiJJRjE1TVRJb1J4dzJFVUVMSlFkdGRMMDdIRFEwUEZySiIsImd0eSI6ImNsaWVudC1jcmVkZW50aWFscyJ9.pWX_QLbNsdnFH1W4T28vUOjDTjBeP_hvUqKD-oYwSLkD48HGPkMGw07dN3JbjACOuwAaPBe0cgtifxtX-PUl6Qj6JJ22BLm7By_ROjsZj5x9XmWiQKf_3hmOISIipG6-kX2iKei4aWGbBIgwLLLNxYZEN-gDSBzmuWjIjTiK7xhMgcfS-t8tzgErF0lE2JaiwN-DllJu9gcYNx3w213k0zH2UtUNR1rnm-cR97fVJa-2Wf8YOgq_aQJvZN_PSQtfrk6nC0zP9f2aJeGp7j432Md3rD_TdM5ioKngXd65DJmIfar861sae96EOBToOk-e-MA_BAFRbu4hEen9VCQBfA",
  "token_type": "Bearer"
}
```

RedIn uses Auth0 Application keys to allow access to the API. To retrieve your access_token you must request it using the example on the right of this screen, or using any http client (curl, guzzlehttp, etc).

RedIn expects for the Authorization header to be included in <strong> all </strong> API requests to the server in a header that looks like the following:

`Authorization: 'Bearer your_access_token_here'`


Once you have your access_token, if you're using axios, you can include it like this for it to be sent in every request:

`axios.defaults.headers.common['Authorization'] = 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik1FUkdRakUzTAiOiJKV1QiLC..etc'`

<aside class="notice">
This access_token will expire every 86400 seconds (24 hours).
</aside>

Another simple way to gather your access_token is with curl

`curl --request POST \
  --url https://fidely.auth0.com/oauth/token \
  --header 'content-type: application/json' \
  --data '{"client_id":"your_static_client_id","client_secret":"your_static_client_secret","audience":"https://api.redin.com.ar","grant_type":"client_credentials"}'`





# Shops/Benefits


## Get All Filters for Shops/Benefits


```javascript
axios.get('http://138.197.65.37/api/v1/shops/rootFilters', {
}).then((res) => {
    this.filters = res.data;
  });
```

> The above command returns JSON structured like this:

```json
{
    "categories": [
        {
            "Nombre": "GASTRONOMIA",
            "IDRubro": 1
        },
        {
            "Nombre": "MODA",
            "IDRubro": 2
        },
        {
            "Nombre": "ENTRETENIMIENTO",
            "IDRubro": 3
        },
    ],
    "subCategories": [
        {
            "Nombre": "JUGUETERÍA",
            "IDRubro": 13,
            "IDRubroPadre": 6
        },
        {
            "Nombre": "RESTAURANTE",
            "IDRubro": 14,
            "IDRubroPadre": 1
        },
        {
            "Nombre": "HELADERÍA",
            "IDRubro": 15,
            "IDRubroPadre": 1
        },
    ],
    "provincies": [
        {
            "Nombre": "BUENOS AIRES",
            "IDProvincia": 1
        },
        {
            "Nombre": "CIUDAD DE BUENOS AIRES",
            "IDProvincia": 2
        },
        {
            "Nombre": "CHUBUT",
            "IDProvincia": 5
        },
    ],
    "cities": [
        {
            "Nombre": "ANDINO",
            "IDCiudad": 1438,
            "IDProvincia": 21
        },
        {
            "Nombre": "SALTO GRANDE",
            "IDCiudad": 1461,
            "IDProvincia": 21
        },
        {
            "Nombre": "SERODINO",
            "IDCiudad": 1465,
            "IDProvincia": 21
        },

    ]
}
```

This endpoint retrieves all the filters needed for listing.

### HTTP Request

`GET http://138.197.65.37/api/v1/shops/rootFilters`


### Returns

Parameter | Description
--------- | -----------
Categories | Available categories of the shops/benefits
Subcategories | Available subcategories of the shops/benefits
Provincies | Available provincies of the shops/Benefits
Cities | Available cities of the shops/benefits


More filters coming soon!



## Get Cities by selected Provincies

```javascript

let provincies = [4, 1, 3];


axios.post('http://138.197.65.37/api/v1/shops/citiesByProvincies', {
    provincies // required
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

> The above command returns JSON structured like this:

```json

  [
       {
           "Nombre": "AVELLANEDA",
           "IDCiudad": 2458
       },
       {
           "Nombre": "MIRAMAR",
           "IDCiudad": 2641
       },
       {
           "Nombre": "AZUL",
           "IDCiudad": 2680
       },
       {
           "Nombre": "WARNES",
           "IDCiudad": 2888
       },
  ]

```

This endpoint retrieves all the cities, per the selected provincies for listing in the filters.

### HTTP Request

`GET http://138.197.65.37/api/v1/shops/index?paginate=20&page=1 `

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- | ---- | --------
provincies | ID's of selected 'IDProvincia' | array of integers | required





## Get Shops/Benefits (paginated/filtered)

```javascript

let paginate = 3;
let page = 1;
let filters = {
  provincies: [1, 2],
  cities: [20900],
  categories: [6, 4]
  textQueryInput: 'Farmacia'
}


axios.post('http://138.197.65.37/api/v1/shops/index', {
  paginate: 3, // required - int - Qty of items to paginate
  page: 1  // required - int - Page the user requested
  filters.provincies  // optional - array of integers -  Get by provincies using the provincies id's gathered in /rootFilters
  filters.cities // optional - array of integers - Get by cities using the cities id's gathered in /rootFilters
  filters.categories  // optional - array of integers - Get by categories using the categories id's gathered in /rootFilters
  filters.textQueryInput // optional - string - Search by user text input - will try to match to the field "NombreFantasia" of Shops/Benefits by using a LIKE comparisson
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

```

> The above command returns JSON structured like this:

```json
{
    "Shops": [
        {
            "NombreFantasia": "SUR MADERAS",
            "IDComercio": 9,
            "Rubro": 6,
            "Provincia": "BUENOS AIRES",
            "IDProvincia": 1,
            "Ciudad": "MAR DEL PLATA",
            "IDCiudad": 20900
        },
        {
            "NombreFantasia": "LOVAAS",
            "IDComercio": 11,
            "Rubro": 6,
            "Provincia": "BUENOS AIRES",
            "IDProvincia": 1,
            "Ciudad": "MAR DEL PLATA",
            "IDCiudad": 20900
        },
        {
            "NombreFantasia": "MUNDO FITNESS",
            "IDComercio": 14,
            "Rubro": 4,
            "Provincia": "BUENOS AIRES",
            "IDProvincia": 1,
            "Ciudad": "MAR DEL PLATA",
            "IDCiudad": 20900
        }
    ]
}
```

This endpoint retrieves all the shops, paginated.


### HTTP Request

`GET http://138.197.65.37/api/v1/shops/index?paginate=20&page=1 `

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- | ---- | --------
paginate | Qty of items to paginate | int | required
page | Page of the user | int | required
filters | Array of filters | array | optional
filters['provincies'] | ID's of selected 'IDProvincia' | Array of integers |  optional
filters['cities'] | ID's of selected 'IDCiudad' | Array of integers |  optional
filters['categories'] | ID's of selected 'IDRubro' | Array of integers |  optional
filters['textQueryInput'] |  User text input | string |  optional


<aside class="warning"> <strong>Important: </strong>  When a new filter search is requested, set the page to 1.</aside>


## Get All Shops/Benefits


```javascript
axios.get('http://138.197.65.37/api/v1/shops/all', {
}).then((res) => {
    this.shops = res.data.Shops;
  });
```

> The above command returns JSON structured like this:

```json
  {
    "Shops": [
        {
            "NombreFantasia": "CASA MAINI",
            "IDComercio": 1727,
            "Rubro": 8,
            "Provincia": "SANTA FE",
            "IDProvincia": 21,
            "Ciudad": "ANDINO",
            "IDCiudad": 1438
        },
        {
            "NombreFantasia": "CASA MAINI",
            "IDComercio": 1729,
            "Rubro": 8,
            "Provincia": "SANTA FE",
            "IDProvincia": 21,
            "Ciudad": "SALTO GRANDE",
            "IDCiudad": 1461
        },
        {
            "NombreFantasia": "CASA MAINI",
            "IDComercio": 1721,
            "Rubro": 8,
            "Provincia": "SANTA FE",
            "IDProvincia": 21,
            "Ciudad": "SERODINO",
            "IDCiudad": 1465
        },
        {
            "NombreFantasia": "BOREAL PINTURAS",
            "IDComercio": 1713,
            "Rubro": 6,
            "Provincia": "SANTA FE",
            "IDProvincia": 21,
            "Ciudad": "GRANADERO BAIGORRIA",
            "IDCiudad": 2078
        }
      ]
  }

```

This endpoint retrieves all the listed shops.


### HTTP Request

`GET http://138.197.65.37/api/v1/shops/all`
