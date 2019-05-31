---
id: version-1.0.0-merchants
title: Merchants
original_id: merchants
---

API URL: `http://api.loyable.it:5000/`

## `/merchants`

---

### GET `/`

| Method                                                                                          | URL          | Response           | Data Type |
| ----------------------------------------------------------------------------------------------- | ------------ | ------------------ | --------- |
| <span style="background-color:#0f6ab4;color:#fff;padding:5px 10px;border-radius:5px">GET</span> | `/merchants` | `application/json` | `Array`   |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| **Authorization** | **true** | Access Token | header | `String` |

**Response**

```js
[
  {
    address: {},
    logo: {},
    style: {},
    _id: "5c9e1d645918590a0d984ebc",
    id: "e61665bf-9d4b-478f-b82c-5db61efd84c1",
    name: "MiNi Sushi",
    description:
      "Lorem, ipsum dolor sit amet consectetur adipisicing elit. Est, blanditiis. Nesciunt, aperiam suscipit? Corrupti quam minima sequi voluptate, vitae neque?",
    cards: []
  },
  {
    address: {},
    logo: {},
    style: {},
    _id: "5c9e54ff3c16e7212e283f60",
    id: "74d1dfde-4219-42a5-bfa8-96b5d0822587",
    name: "Spontini - Papiniano",
    description:
      "Con l'apertura di Via Arona, 15 a Milano, la seconda in una settimana, Spontini arriva a 30 locali fra Italia e Estero. Il nuovo store è aperto dalle 8 con il servizio colazione.",
    cards: []
  }
];
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**200**</span> | Success | `[ merchant: Merchant ]`|
| <span style="color:#ffe433">**401**</span> | Unauthorized | `{ error: 401, message: "Unauthorized" }`|
| <span style="color:orange">**403**</span> | Forbidden | `{ error: 403, message: "Forbidden" }`|
| <span style="color:red">**404**</span> | Not Found | `{ error: 404, message: "Not Found" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> Only available to admins for Data Analysis

---

### GET `/{merchantID}`

| Method                                                                                          | URL                       | Response           | Data Type |
| ----------------------------------------------------------------------------------------------- | ------------------------- | ------------------ | --------- |
| <span style="background-color:#0f6ab4;color:#fff;padding:5px 10px;border-radius:5px">GET</span> | `/merchants/{merchantID}` | `application/json` | `Object`  |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| `merchantID` | **true** | Merchant ID | path | `String` |
| **Authorization** | **true** | Access Token | header | `String` |

**Response**

```js
{
  address: {
    location: {
      type: "Point",
      coordinates: [
        45.4580139,
        9.1703518
      ]
    },
    value: "Viale Papiniano, 43, 20123 Milano MI"
  },
  logo: {
    backgroundColor: "#b40001",
    src: "http://www.pizzeriaspontini.it//graphic/headLogo.png",
    width: 130,
    height: 60
  },
  style: {
    address: {
    fontSize: 16,
    textAlign: "left",
    color: "#8e8e8e",
    fontStyle: "normal",
    fontWeight: "normal"
    },
    title: {
    fontSize: 22,
    textAlign: "left",
    color: "#3c3c3c",
    fontStyle: "normal",
    fontWeight: "normal"
    }
  },
  _id: "5c9e54ff3c16e7212e283f60",
  id: "74d1dfde-4219-42a5-bfa8-96b5d0822587",
  name: "Spontini - Papiniano",
  description: "Con l'apertura di Via Arona, 15 a Milano, la seconda in una settimana, Spontini arriva a 30 locali fra Italia e Estero. Il nuovo store è aperto dalle 8 con il servizio colazione.",
  cards: [
    {
      _id: "5c9e54ff3c16e7212e283f61",
      id: "271cca4e-14e4-46c2-93c3-79ef70ee3284"
    }
  ],
}
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**200**</span> | Success | [`Merchant`](#merchant)|
| <span style="color:#ffe433">**401**</span> | Unauthorized | `{ error: 401, message: "Unauthorized" }`|
| <span style="color:orange">**403**</span> | Forbidden | `{ error: 403, message: "Forbidden" }`|
| <span style="color:red">**404**</span> | Not Found | `{ error: 404, message: "Merchant Not Found" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> Gather information about the merchant

---

### POST `/`

| Method                                                                                           | URL          | Response           | Data Type |
| ------------------------------------------------------------------------------------------------ | ------------ | ------------------ | --------- |
| <span style="background-color:#10a54a;color:#fff;padding:5px 10px;border-radius:5px">POST</span> | `/merchants` | `application/json` | `Object`  |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| [`Merchant`](#merchant) | **true** | Merchant Object | body | `String` |
| **Authorization** | **true** | Access Token | header | `String` |

**Request Body**

```js
{
	"address": { // required
		"value": "Via Firenze, 51/52, 00184 Roma RM",
		"location": {
			"type": "Point",
			"coordinates": [
				41.9008794,
				12.4950295
			]
		}
	},
	"logo": { //required
		"backgroundColor": "rgb(45,32,12)",
		"src": "https://i.ibb.co/J23Pnwf/logoilfornodegliamici.png",
		"width": 640,
		"height": 333
	},
	"name": "Il Forno degli Amici", // required
	"description": "Non c’è ne lievito madre qui, tantomeno il lievito di birra, abbiamo catturato i lieviti selvaggi e li abbiamo fatti lavorare nel nostro pane, profumo, forma e sapore....",
	"cards": []
}
```

**Response**

```js
{
  "address": {
    "location": {
      "type": "Point",
      "coordinates": [
        41.9008794,
        12.4950295
      ]
    },
    "value": "Via Firenze, 51/52, 00184 Roma RM"
  },
  "logo": {
    "backgroundColor": "rgb(45,32,12)",
    "src": "https://i.ibb.co/J23Pnwf/logoilfornodegliamici.png",
    "width": 640,
    "height": 333
  },
  "style": {
    "address": {
      "fontSize": 16,
      "textAlign": "left",
      "color": "#8e8e8e",
      "fontStyle": "normal",
      "fontWeight": "normal"
    },
    "title": {
      "fontSize": 22,
      "textAlign": "left",
      "color": "#3c3c3c",
      "fontStyle": "normal",
      "fontWeight": "normal"
    }
  },
  "_id": "5cafb3902455cf1b831d8821",
  "id": "d2b8ec22-fd1b-477e-b514-e14a2fe399b9",
  "name": "Il Forno degli Amici",
  "description": "Non c’è ne lievito madre qui, tantomeno il lievito di birra, abbiamo catturato i lieviti selvaggi e li abbiamo fatti lavorare nel nostro pane, profumo, forma e sapore....",
  "cards": []
}
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**201**</span> | Resource Created | [`Merchant`](#merchant)|
| <span style="color:#ffe433">**401**</span> | Unauthorized | `{ error: 401, message: "Unauthorized" }`|
| <span style="color:orange">**403**</span> | Forbidden | `{ error: 403, message: "Forbidden" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> Only available by admins

---

### PATCH `/{merchantID}`

| Method                                                                                            | URL                       | Response           | Data Type |
| ------------------------------------------------------------------------------------------------- | ------------------------- | ------------------ | --------- |
| <span style="background-color:#d38042;color:#fff;padding:5px 10px;border-radius:5px">PATCH</span> | `/merchants/{merchantID}` | `application/json` | `Object`  |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| `merchantID` | **true** | Merchant ID | path | `String` |
| [`Merchant`](#merchant) | **true** | User Object | body | `Object` |
| **Authorization** | **true** | Access Token | header | `String` |

**Request Body** (All [`Merchant`](#merchant) properties are **NOT** required)

```js
{
    "address": {
        "value": "Via Firenze, 51/52, 00184 Roma RM",
        "location": {
            "type": "Point",
            "coordinates": [
                41.9008794,
                12.4950295
            ]
        }
    }
}
```

**Response** ([`Merchant`](#merchant) object updated)

```js
{
  "address": {
    "location": {
      "type": "Point",
      "coordinates": [
        41.9008794,
        12.4950295
      ]
    },
    "value": "Via Firenze, 51/52, 00184 Roma RM"
  },
  "logo": {
    "backgroundColor": "rgb(45,32,12)",
    "src": "https://i.ibb.co/J23Pnwf/logoilfornodegliamici.png",
    "width": 640,
    "height": 333
  },
  "style": {
    "address": {
      "fontSize": 16,
      "textAlign": "left",
      "color": "#8e8e8e",
      "fontStyle": "normal",
      "fontWeight": "normal"
    },
    "title": {
      "fontSize": 22,
      "textAlign": "left",
      "color": "#3c3c3c",
      "fontStyle": "normal",
      "fontWeight": "normal"
    }
  },
  "_id": "5cafb3902455cf1b831d8821",
  "id": "d2b8ec22-fd1b-477e-b514-e14a2fe399b9",
  "name": "Il Forno degli Amici",
  "description": "Non c’è ne lievito madre qui, tantomeno il lievito di birra, abbiamo catturato i lieviti selvaggi e li abbiamo fatti lavorare nel nostro pane, profumo, forma e sapore....",
  "cards": []
}
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**200**</span> | Success | [`Merchant`](#merchant)|
| <span style="color:#ffe433">**401**</span> | Unauthorized | `{ error: 401, message: "Unauthorized" }`|
| <span style="color:orange">**403**</span> | Forbidden | `{ error: 403, message: "Forbidden" }`|
| <span style="color:red">**404**</span> | Not Found | `{ error: 404, message: "Merchant Not Found" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> To update merchant information. All [`Merchant`](#merchant) fields are not required

---

### DELETE `/{merchantID}`

| Method                                                                                             | URL                       | Response           | Data Type |
| -------------------------------------------------------------------------------------------------- | ------------------------- | ------------------ | --------- |
| <span style="background-color:#a41e22;color:#fff;padding:5px 10px;border-radius:5px">DELETE</span> | `/merchants/{merchantID}` | `application/json` | `Object`  |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| `merchantID` | **true** | Merchant ID | path | `String` |
| **Authorization** | **true** | Access Token | header | `String` |

**Response**

```js
{
  merchantID: Merchant.id,
  message: "Merchant deleted"
}
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**204**</span> | Resource Deleted | `{ merchantID: Merchant.id, message: "Merchant deleted" }`|
| <span style="color:#ffe433">**401**</span> | Unauthorized | `{ error: 401, message: "Unauthorized" }`|
| <span style="color:orange">**403**</span> | Forbidden | `{ error: 403, message: "Forbidden" }`|
| <span style="color:red">**404**</span> | Not Found | `{ error: 404, message: "Merchant Not Found" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> Be careful! `Merchant` data cannot be recovered!

---

## Object Types

---

### `Merchant`

```js
{
    id: {
      type: String,
      required: true,
      unique: true,
      index: true,
      default: uuid()
    },
    name: { type: String, required: true },
    address: {
      value: { type: String, required: true },
      location: {
        type: {
          type: String,
          enum: ["Point"],
          default: "Point",
          required: true
        },
        coordinates: {
          type: [Number],
          required: true
        }
      },
      geohash: {
        type: String,
        required: true
      }
    },
    description: String,
    logo: {
      src: { type: String, required: true },
      width: { type: Number, required: true },
      height: { type: Number, required: true },
      backgroundColor: { type: String, required: true, default: "transparent" }
    },
    cards: [
      {
        id: {
          type: String,
          required: true
        },
        card: {}
      }
    ],
    style: {
      address: {
        fontSize: {
          type: Number,
          default: 16
        },
        textAlign: {
          type: String,
          default: "left"
        },
        color: {
          type: String,
          default: "#000"
        },
        fontStyle: {
          type: String,
          default: "normal"
        },
        fontWeight: {
          type: String,
          default: "normal"
        },
        lineHeight: {
          type: Number
        },
        letterSpacing: {
          type: Number
        }
      },
      title: {
        fontSize: {
          type: Number,
          default: 22
        },
        fontFamily: {
          type: String
        },
        textAlign: {
          type: String,
          default: "left"
        },
        color: {
          type: String,
          default: "#000"
        },
        fontStyle: {
          type: String,
          default: "normal"
        },
        fontWeight: {
          type: String,
          default: "normal"
        },
        lineHeight: {
          type: Number
        },
        letterSpacing: {
          type: Number
        }
      }
    }
  }
```
