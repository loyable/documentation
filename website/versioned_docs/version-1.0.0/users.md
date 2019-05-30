---
id: version-1.0.0-users
title: Users
original_id: users
---

API URL: `http://api.loyable.it:5000/`

## `/users`

---

### GET `/`

| Method                                                                                          | URL      | Response           | Data Type |
| ----------------------------------------------------------------------------------------------- | -------- | ------------------ | --------- |
| <span style="background-color:#0f6ab4;color:#fff;padding:5px 10px;border-radius:5px">GET</span> | `/users` | `application/json` | `Array`   |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| **Authorization** | **true** | Access Token | header | `String` |

**Response**

```js
[
  {
    id: "4048ed6b-bcad-4e73-9852-1ba4c585acdb", // uuidv4
    created: "2019-04-11T07:48:27.539Z", // date of user first registration
    _id: "5cafb4262455cf1b831d8824", // MongoDB Object ID
    phone: "+393391848457", // phone number with prefix
    merchants: [
      {
        cards: [
          {
            id: "73484a86-e233-438f-a007-d2fd0a32a34a", // card ID
            marked: 9, // stamps marked
            hidden: false, // true if card is hidden
            created: "2019-04-11T07:48:27.539Z", // date of card creation
            history: [
              // card history
              {
                value: "+1",
                time: "2019-04-11T07:48:27.539Z",
                _id: "5cafb4262455cf1b831d8835",
                type: "add" // history type
              }
            ],
            _id: "5cafb4262455cf1b831d8834",
            designID: "62db33d8-bc6e-4864-b50f-281aab7c9893" // card design ID
          }
        ],
        history: [
          // merchant history
          {
            value: "+1",
            time: "2019-04-11T07:48:27.539Z",
            _id: "5cafb4262455cf1b831d8836",
            type: "completed" // history type
          }
        ],
        _id: "5cafb4262455cf1b831d8831",
        merchantID: "e61665bf-9d4b-478f-b82c-5db61efd84c1" // merchantID
      }
    ],
    verificationHash: "1e6a1a38879998edd2dc43fdbc7cc660" // last SMS verification hash
  }
];
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**200**</span> | Success | `[ user: User ]`|
| <span style="color:#ffe433">**401**</span> | Unauthorized | `{ error: 401, message: "Unauthorized" }`|
| <span style="color:orange">**403**</span> | Forbidden | `{ error: 403, message: "Forbidden" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> Only available to admins for Data Analysis

---

### GET `/{userID}`

| Method                                                                                          | URL               | Response           | Data Type |
| ----------------------------------------------------------------------------------------------- | ----------------- | ------------------ | --------- |
| <span style="background-color:#0f6ab4;color:#fff;padding:5px 10px;border-radius:5px">GET</span> | `/users/{userID}` | `application/json` | `Object`  |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| `userID` | **true** | User ID | path | `String` |
| **Authorization** | **true** | Access Token | header | `String` |

**Response**

```js
{
  user: {
    id: "4048ed6b-bcad-4e73-9852-1ba4c585acdb", // uuidv4
    phone: "+393391848457", // phone number with prefix
    created: "2019-04-11T07:48:27.539Z", // date of user first registration
    merchants: [] // merchants array
  },
  hash: "3449c9e5e332f1dbb81505cd739fbf3f" // md5 hash of the user
}
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**200**</span> | Success | `{ user: User, hash: MD5 }`|
| <span style="color:#ffe433">**401**</span> | Unauthorized | `{ error: 401, message: "Unauthorized" }`|
| <span style="color:orange">**403**</span> | Forbidden | `{ error: 403, message: "Forbidden" }`|
| <span style="color:red">**404**</span> | Not Found | `{ error: 404, message: "User not found" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> Gather information about the user

---

### POST `/`

| Method                                                                                           | URL      | Response           | Data Type |
| ------------------------------------------------------------------------------------------------ | -------- | ------------------ | --------- |
| <span style="background-color:#10a54a;color:#fff;padding:5px 10px;border-radius:5px">POST</span> | `/users` | `application/json` | `Object`  |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| `phone` | **true** | Phone number | body | `String` |
| `merchants` | false | Merchants Array | body | `Array` |
| **Authorization** | **true** | Access Token | header | `String` |

**Request Body**

```js
{
  "phone": "+393357898922"
}
```

**Response**

```js
{
  "id": "f4d806bb-370a-4db1-a344-b51630b8340c", // uuidv4 generated
  "created": "2019-05-30T15:49:28.456Z", // automatically added
  "_id": "5ceffb8c72a5dc17035d962f", // MongoDB Object ID
  "phone": "+393357898922",
  "merchants": [], // empty merchant array
}
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**201**</span> | Resource Created | [`User`](#user)|
| <span style="color:#ffe433">**401**</span> | Unauthorized | `{ error: 401, message: "Unauthorized" }`|
| <span style="color:orange">**403**</span> | Forbidden | `{ error: 403, message: "Forbidden" }`|
| <span style="color:red">**422**</span> | Unprocessable Entity | `{ error: 422, message: "User already registered" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> Only available by admins (use [`/auth`](auth) to register a user instead)

---

### PATCH `/{userID}`

| Method                                                                                            | URL               | Response           | Data Type |
| ------------------------------------------------------------------------------------------------- | ----------------- | ------------------ | --------- |
| <span style="background-color:#d38042;color:#fff;padding:5px 10px;border-radius:5px">PATCH</span> | `/users/{userID}` | `application/json` | `Object`  |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| `userID` | **true** | User ID | path | `String` |
| [`User`](#user) | **true** | User Object | body | `Object` |
| **Authorization** | **true** | Access Token | header | `String` |

**Request Body** (All [`User`](#user) properties are **NOT** required)

```js
{
  id: "4048ed6b-bcad-4e73-9852-1ba4c585acdb", // uuidv4
  phone: "+393391848457", // phone number with prefix
  created: "2019-04-11T07:48:27.539Z", // date of user first registration
  merchants: [] // merchants array
}
```

**Response** ([`User`](#user) object updated)

```js
{
  id: "4048ed6b-bcad-4e73-9852-1ba4c585acdb", // uuidv4
  phone: "+393391848457", // phone number with prefix
  created: "2019-04-11T07:48:27.539Z", // date of user first registration
  merchants: [] // merchants array
}
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**200**</span> | Success | [`User`](#user)|
| <span style="color:#ffe433">**401**</span> | Unauthorized | `{ error: 401, message: "Unauthorized" }`|
| <span style="color:orange">**403**</span> | Forbidden | `{ error: 403, message: "Forbidden" }`|
| <span style="color:red">**404**</span> | Not Found | `{ error: 404, message: "User Not Found" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> To update user information. All [`User`](#user) fields are not required

---

### DELETE `/{userID}`

| Method                                                                                             | URL               | Response           | Data Type |
| -------------------------------------------------------------------------------------------------- | ----------------- | ------------------ | --------- |
| <span style="background-color:#a41e22;color:#fff;padding:5px 10px;border-radius:5px">DELETE</span> | `/users/{userID}` | `application/json` | `Object`  |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| `userID` | **true** | User ID | path | `String` |
| **Authorization** | **true** | Access Token | header | `String` |

**Response**

```js
{
  userID: User.id,
  message: "User deleted"
}
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**204**</span> | Resource Deleted | `{ userID: User.id, message: "User deleted" }`|
| <span style="color:#ffe433">**401**</span> | Unauthorized | `{ error: 401, message: "Unauthorized" }`|
| <span style="color:orange">**403**</span> | Forbidden | `{ error: 403, message: "Forbidden" }`|
| <span style="color:red">**404**</span> | Not Found | `{ error: 404, message: "User Not Found" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> Be careful! `User` data cannot be recovered!

---

## Object Types

---

### `User`

```js
{
  id: {
    type: String,
    required: true,
    unique: true,
    index: true,
    default: uuid()
  },
  phone: {
    type: String,
    required: true,
    unique: true
  },
  verificationHash: {
    type: String
  },
  created: {
    type: Date,
    default: Date.now()
  },
  merchants: [
    {
      merchantID: {
        type: String,
        required: true
      },
      merchant: {},
      cards: [
        {
          id: {
            type: String,
            required: true,
            default: uuid()
          },
          designID: {
            type: String,
            required: true
          },
          card: {},
          marked: {
            type: Number,
            default: 0
          },
          hidden: {
            type: Boolean,
            default: false
          },
          created: {
            type: Date,
            default: Date.now()
          },
          history: [
            {
              type: {
                type: String
              },
              value: {
                type: String,
                default: "+1"
              },
              time: {
                type: Date,
                default: Date.now()
              }
            }
          ]
        }
      ],
      history: [
        {
          type: {
            type: String
          },
          value: {
            type: String,
            default: "+1"
          },
          time: {
            type: Date,
            default: Date.now()
          }
        }
      ]
    }
  ]
}
```
