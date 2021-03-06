---
title: Get a customer's subscriptions
description: How to get a collection of a customer's subscriptions.
ms.assetid: 1C9E986B-2887-460B-9D71-4520BB18C32A
ms.date: 12/15/2017
ms.localizationpriority: medium
---

# Get a customer's subscriptions


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

How to get a collection of a customer's subscriptions.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A customer identifier.

## <span id="C_"></span><span id="c_"></span>C#


To get a list of all of a customer's subscriptions, first use the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to identify the customer. Then use the [**Subscriptions**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations. Finally, call the [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) methods to retrieve the customer's subscriptions collection.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerSubscriptions = partnerOperations.Customers.ById(customerId).Subscriptions.Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: GetSubscriptions.cs

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request


**Request syntax**

| Method  | Request URI                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1 |

 

**URI parameter**

This table lists the required query parameter to get all the subscriptions.

| Name               | Type   | Required | Description                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| customer-tenant-id | string | Yes      | A GUID-formatted string that identifies the customer. |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

None.

**Request example**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, this method returns a collection of [Subscription](subscriptions.md) resources in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
Date: Wed, 25 Nov 2015 05:43:06 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de", 
        "entitlementId": "a356ac8c-e310-44f4-bf85-C7f29044af99",
        "friendlyName": "nickname",
        "quantity": 1,
        "unitType": "none",
        "creationDate": "2015-11-25T06: 41: 12Z",
        "effectiveStartDate": "2015-11-24T08: 00: 00Z",
        "commitmentEndDate": "2016-12-12T08: 00: 00Z",
        "status": "active",
        "autoRenewEnabled": false,
        "billingType": "none",
        "contractType": "subscription",
        "links": {
            "offer": {
                "uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        },
        "orderId": "6183db3d-6318-4e52-877e-25806e4971be",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Subscription"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 




