---
id: version-1.0.0-auth
title: Auth
original_id: auth
---

**Verification code expiration:** 10 minutes

## `/auth`

---

### `/{phone}`

| Method                                                                                          | URL             | Response           | Data Type |
| ----------------------------------------------------------------------------------------------- | --------------- | ------------------ | --------- |
| <span style="background-color:#0f6ab4;color:#fff;padding:5px 10px;border-radius:5px">GET</span> | `/auth/{phone}` | `application/json` | `Object`  |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| `phone` | **true** | Phone Number | path | `String` |

**Response**

```js
{
  success: true,
  message: "SMS Sent"
}
```

**Response if token is not expired**

```js
{
  expired: false,
  remaining: Number //Minutes
}
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**200**</span> | Success | `{ success: true, message: "SMS Sent" }`|
| <span style="color:red">**404**</span> | Not Found | `{ error: 404, message: "Not Found" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> Send SMS with verification code

---

### `/{phone}/verify/{code}`

| Method                                                                                          | URL                           | Response           | Data Type |
| ----------------------------------------------------------------------------------------------- | ----------------------------- | ------------------ | --------- |
| <span style="background-color:#0f6ab4;color:#fff;padding:5px 10px;border-radius:5px">GET</span> | `/auth/{phone}/verify/{code}` | `application/json` | `Object`  |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| `phone` | **true** | Phone Number | path | `String` |
| `code` | **true** | Verification Code | path | `Number` |

**Response**

```js
{
  id: "4048ed6b-bcad-4e73-9852-1ba4c585acdb",
  token: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjQwNDhlZDZiLWJjYWQtNGU3My05ODUyLTFiYTRjNTg1YWNkYiIsImlhdCI6MTU1OTMwOTY4NX0.bFnM8hy5fPgW7_omZ3qIRj81i7kFFJU0xqHXwfbbyb4"
}
```

**Response if verification code is incorrect**

```js
{
  id: "",
  token: ""
}
```

**Response if session is expired**

```js
{
  expired: true;
}
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**200**</span> | Success | `{ id: User.id, token: Session }` or `{ id: "", token: "" }` or `{ expired: true }` |
| <span style="color:red">**404**</span> | Not Found | `{ error: 404, message: "Not Found" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> Verify the code & generate Session token

---

### `/{phone}/change/{code}/{newPhone}`

| Method                                                                                          | URL                                      | Response           | Data Type |
| ----------------------------------------------------------------------------------------------- | ---------------------------------------- | ------------------ | --------- |
| <span style="background-color:#0f6ab4;color:#fff;padding:5px 10px;border-radius:5px">GET</span> | `/auth/{phone}/change/{code}/{newPhone}` | `application/json` | `Object`  |

**Parameters**
| Parameter | Required | Description | Parameter Type | Data Type |
|-----------|-------|-------------|----------------|-----------|
| `phone` | **true** | Phone Number | path | `String` |
| `code` | **true** | Verification Code | path | `Number` |
| `newPhone` | **true** | New Phone Number | path | `String` |

**Response**

```js
{
  success: true,
  message: "User Phone Changed"
}
```

**Response if user is already registered**

```js
{
  success: false,
  message: "User Already Registered"
}
```

**Response if verification code is incorrect**

```js
{
  success: false,
  message: "Wrong Verification Code"
}
```

**Response if session is expired**

```js
{
  expired: true;
}
```

**Response Messages**
| Status | Reason | Response Model
|-----------|-------|-------------|
| <span style="color:green">**200**</span> | Success | `{ success: true, message: "User Phone Changed" }` or `{ expired: true }` |
| <span style="color:red">**404**</span> | Not Found | `{ error: 404, message: "Not Found" }`|
| <span style="color:violet">**500**</span> | Internal Server Error | `{ error: 500, message: "Internal Server Error" }`|

**Notes**

> Change phone number

---
