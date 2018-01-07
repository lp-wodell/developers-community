---
title: Audit Trail
level1: Documents
level2: Account Configuration
level3: Meta Data
level4: Methods

permalink: account-configuration-meta-data-audit-trail.html
order: 50
indicator: both
---

Get account's audit trail records

### Request

| Method | URL |
| :-------- | :------ |
| POST | /api/account/{accountId}/configuration/metadata/audit |

**Request Headers**

| Header | Description |
| :------- | :-------------- |
|Authorization | Contains token string to allow request authentication and authorization. See the introduction doc for more details. |

**Path Parameters**

|Parameter|  Description|  Type|  Notes| 
|:----------|  :--------------|  :--------------|  :---| 
|accountId|  LP site ID|  string ^[a-zA-Z0-9_]{1,20}$|  Validation fail error code: 400 |

**Query Parameters**

N/A

**Request Body**

Contains a json object with single "query" field which define the requested graphql query for api auditData
and the fields subselect. For details see [graphql website](http://graphql.org/)

```json
{"query" : "{auditData  
              {accountId 
              objectType 
              objectName 
              actionType 
              element 
              oldValue 
              newValue 
              changeDate 
              originator 
              originatorLoginName 
              originatorUserId 
              originatorUserAgent 
              originatorAuthType 
              originatorIsLpa}}"}
```

**Optional graphql parameters**

|name|Description|Notes|
| :--- | :--- | :--- |
|fromDate|Start date for filtering|Format: yyyy-MM-dd|
|toDate|End date for filtering|Format: yyyy-MM-dd|
|first|Number of records to return|Default: 50|
|offset|Offset to start returning records from||
|orderBy|List of columns to order by|Default: changeTimestamp|
|orderDirection|List of ordering direction(ASC, DESC), in relevance to orderBy list|Default: DESC|
|users|List of users for filtering||
|componentTypes|List of component types for filtering||
|language|Language to return the results in|Default: en-US|
|timezone|Time zone to use in results|Default: US/Eastern|
|lpa|Boolean, Include changes done by LPAs in the results|Default: false|
|automaticUpdates|Boolean, Include automatic updates in the results|Default: false|

### Response

**Response type**

JSON

**Response Headers**

|Header|Description|
| :--- | :--- |
|X-Total-Count|Contains the count of returned audit items|

**Response Codes**

| Code | Description |
| :----- | :------------ |
| 200 | OK |
| 400 | Bad Request |
| 401 | Not Authenticated |
| 403 | Not Authorized |
| 500 | Internal Server Error |


**Response Body**

```json
{
  "data": {
    "auditData": [
        {
        "accountId": "le33192344",
        "objectType": "Users",
        "objectName": "objectName1",
        "actionType": "Edit",
        "element": "property",
        "oldValue": "oldValue",
        "newValue": "newValue",
        "changeDate": "2017-12-04 08:13:34.0",
        "originator": "user name",
        "originatorLoginName": "loginName",
        "originatorUserId": "userId_1",
        "originatorUserAgent": "userAgent",
        "originatorAuthType": "auth1",
        "originatorIsLpa": false
      }
    ]
}
```
