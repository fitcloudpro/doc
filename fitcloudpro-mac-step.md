# FitCloudPro server data transmission interface

## 1. Description
The document interface data uses the `http` request method, and the returned data format is unified as` json`.

Examples of returned data are as follows:
```json
{
    "errorCode": 0,
    "errorMsg": "",
    "data": {
        "rows": 31099, // list size of results
        "pageNo": 1, // current page number
        "pageSize": 100, // rows per page
        "results": [] // result array
    }
}
```

## 2. Data interface

Interface name: /transfer/mac-step
Interface role: return sum steps of user who bind their device to phone and uploaded within 15 days
Interface parameters:
| Parameter | Type | Required | Description |
|-|-|-|-|
| accessToken | String | Yes | fitcloud provides |
| page | Integer | No | Page number, starting from 1, default: 1 |
| pageSize | Integer | No | Number of records per page, default: 5000, maximum 5000 |


return value:  
| Back Field | Type | Description |
|-|-|-|
| errorCode | int | Error code, 0 means success, other values ​​mean failure. The failure value is determined according to the error type of the actual interface. |
| errorMsg | String | Error description. When errorCode is 0, this field is empty. |
| data | String | Data packet structure |

```json
data: {
    "pageNo": 1,
    "pageSize": 5000,
    "rows": 401,
    "results": [
      {
        "row_number": 1,                                // just a row number
        "request_time": "2020-05-24 23:07:06",          // request time
        "email": "47matej@gmail.com",                   // email bind with mac
        "mac_address": "AC:2A:21:B0:80:8F",             // mac address of user device
        "step": 4550,                                   // total steps in 15 days upon request time
        "first_bind_time": "2020-05-24 14:09:55"        // first time when this device has been recorded
      },
      {
        "row_number": 2,
        "request_time": "2020-05-24 23:07:06",
        "email": "adamnasos@gmail.com",
        "mac_address": "AC:2A:21:B0:8F:8A",
        "step": 2355,
        "first_bind_time": "2020-05-24 14:21:53"
      },
      {
        "row_number": 3,
        "request_time": "2020-05-24 23:07:06",
        "email": "a.desimone@gmx.de",
        "mac_address": "AC:2A:21:B0:4B:38",
        "step": 3617,
        "first_bind_time": "2020-05-24 16:36:10"
      },
      ...
}      
```

## 3. Example with test key

https://fitcloud.hetangsmart.com/transfer/mac-step?accessToken=5c168ef82b1b4dd89d24637045739881