# GeoAdminApi3.js

This collection currently contains four functions. These functions are designed to interact with the [geo.admin Api3](https://api3.geo.admin.ch).

To test the functions implemented in this js file. I exported the postman json collection I used and added to this repo (GeoAdminApi.postman_collection.json).

## Overview

The four functions are:
```js
async function isValidAddress(searchString);

async function getNumberOfResults(searchString);

async function getListCoordinates(searchString);

async function getRequest(url)
```

## Functions

### `getRequest(url)`

This function is the basic GET request function. The get request will be sent to the **url** and the response will be server response will be parsed and returns as an **json** object.
### Example: 
#### Request: https://api3.geo.admin.ch/1912100956/rest/services/ech/SearchServer?sr=2056&searchText=Peterliwiese33&lang=en&type=locations

#### Response: json
```json
{
    "results": [
        {
            "id": 457481311,
            "weight": 14,
            "attrs": {
                "origin": "address",
                "geom_quadindex": "030031230120230333113",
                "zoomlevel": 10,
                "featureId": "3087703_0",
                "lon": 8.88730239868164,
                "detail": "peterliwiese 33 8855 wangen sz 1349 wangen _sz_ ch sz",
                "rank": 7,
                "geom_st_box2d": "BOX(2709775.421 1228079.091,2709775.421 1228079.091)",
                "lat": 47.194541931152344,
                "num": 33,
                "y": 2709775.5,
                "x": 1228079.125,
                "label": "Peterliwiese 33 <b>8855 Wangen SZ</b>"
            }
        }
    ]
}
```



### `getListCoordinates(searchString)`

This function will return all the results found with the provided **searchString**. Internally this function will build the url and call the `getRequest`function.

### Example: 
#### searchString: "Peterliwiese 33"
*spaces will be encoded!*

#### Response: List
```json
[
    {
        "id": 457481311,
        "weight": 14,
        "attrs": {
            "origin": "address",
            "geom_quadindex": "030031230120230333113",
            "zoomlevel": 10,
            "featureId": "3087703_0",
            "lon": 8.88730239868164,
            "detail": "peterliwiese 33 8855 wangen sz 1349 wangen _sz_ ch sz",
            "rank": 7,
            "geom_st_box2d": "BOX(2709775.421 1228079.091,2709775.421 1228079.091)",
            "lat": 47.194541931152344,
            "num": 33,
            "y": 2709775.5,
            "x": 1228079.125,
            "label": "Peterliwiese 33 <b>8855 Wangen SZ</b>"
        }
    }
]
```

### `getNumberOfResults(searchString)`

This function will return the number of results found with the provided **searchString**. Internally call the `getListCoordinates`function and returns the length of the result.

### Example: 
#### searchString: "Peterliwiese 33"
*spaces will be encoded!*

#### Response: List
```json
1
```
### `isValidAddress(searchString)`

This function will return the number of results found with the provided **searchString**. Internally call the `getNumberOfResults`function and if the result has only one element it will return true.

### Example: 
#### searchString: "Peterliwiese 33"
*spaces will be encoded!*

#### Response: List
```json
true
```

## Usage

I wrote a small HTML page (example.html) to show how to call the functions. The results of the calls wil be outputted to the console.

### import `GeoAdminApi3.js`
```html
<script src="GeoAdminApi3.js"></script>
```
### call a function
```js
let searchString = document.getElementById("getListCoordinatesTextField").value;
let result = await getListCoordinates(searchString);
console.log(result);
//Do Stuff with the result!
```