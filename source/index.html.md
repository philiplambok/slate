---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

includes:
  - errors

search: true
---

# Introduction

Welcome to the Mekari Payment API!

# Authentication

> Example usage of authentication API 

```shell
curl --request GET \
  --url https://payment-service-production.cd.jurnal.id/api/v2/invoices/10ffb09a-2b3d-497d-a55e-60bbc3d8dddd \
  --header 'authorization: 24e9f230458541fb8f0c74c97734d000' \
  --header 'content-type: application/json'
```

Mekari payment API use `authorization` key headers for the authentication. So the authentication format will be `authorization: {your_api_token}`.

You should includes this `authorization` headers key to all request in mekari payment API.

# Invoices

## Create New Invoice

The enpoint for create a new invoice.

```shell
POST /api/v2/invoices
```

### Create Invoice Request 

> Example of create invoice request:

```json
{
  "external_id": "invoice-sample-production-001",
  "amount": 500000,
  "description": "This is first sample invoice",
  "due_date": "2010-05-20",
  "company_name": "Mekari",
  "customer_name": "Bill John",
  "customer_email": "bill.john@mekari.com",
  "customer_phone": "08123123123"
}
```

Parameter | Description
--------- |  -----------
external_id | `string` An ID of your choice.
amount |  `number` Amount end-customer will pay. 
description | `string` The invoice description.
due_date | `string` The invoice due date. Follows format: `YYYY-MM-DD`
company_name | `string` The company name who created the invoice.
customer_name | `string` The customer name who created the invoice.
customer_email | `string` The customer email who created the invoice. <br> System will use this field to send email when payment was received.  
customer_phone | `string` Phone number of customer. (e.g. 08123123123)

### Create Invoice Response

> Example of create invoice response:

```json
{
  "data": {
    "id": "10ffb09a-2b3d-497d-a55e-60bbc3d8dddd",
    "type": "invoice",
    "attributes": {
      "uuid": "10ffb09a-2b3d-497d-a55e-60bbc3d8dddd",
      "external_id": "invoice-sample-production-001",
      "amount_formatted": "Rp 500.000,00",
      "description": "This is first sample invoice",
      "due_date": "2010-05-20T00:00:00.000Z",
      "due_date_formatted": "20/05/2010",
      "company_name": "Mekari",
      "customer_name": "Bill John",
      "customer_email": "bill.john@mekari.com",
      "customer_phone": "08123123123",
      "status": "unpaid"
    }
  },
  "links": {
    "self": "https://payment-service-production.cd.jurnal.id/web/invoices/10ffb09a-2b3d-497d-a55e-60bbc3d8dddd"
  }
}
```

Parameter | Description
--------- |  -----------
uuid | `string` The invoice ID.
external_id | `string` An ID of your choice.
amount_formatted | `string` Invoice amount with formatted presentation.
description | `string` The invoice description.
due_date | `string` The invoice due date.
due_date_formatted | `string` The invoice due date with formatted persentation. The format will follows: DD/MM/YYY.
company_name | `string` The company's name who created the invoice.
customer_name | `string` The customer's name who created the invoice.
customer_email | `string` The customer's email who created the invoice.
customer_phone | `string` Phone number of customer. (e.g. 08123123123)
status | `string` The current status of invoice. 
links | `Object` Link of invoice payment page.

### Create Invoice Errors

List of posible error

```json
{
  "errors": [
    {
      "code": "RecordInvalid",
      "title": "external_id is invalid",
      "details": "external_id sudah digunakan"
    }
  ]
}
```

Name  | Description
--------- | -----------
RecordInvalid | Inputs are failing validation. The errors field contains details about which fields are violating validation.

## Get a Specific Invoice

The endpoint for show a spesific invoice detail.

```shell
GET /api/v2/invoices/:uuid
```

> Example of get a specific invoice response:

```json
{
  "data": {
    "id": "10ffb09a-2b3d-497d-a55e-60bbc3d8dddd",
    "type": "invoice",
    "attributes": {
      "uuid": "10ffb09a-2b3d-497d-a55e-60bbc3d8dddd",
      "external_id": "invoice-sample-production-001",
      "amount_formatted": "Rp 500.000,00",
      "description": "This is first sample invoice",
      "due_date": "2010-05-20T00:00:00.000Z",
      "due_date_formatted": "20/05/2010",
      "company_name": "Mekari",
      "customer_name": "Bill John",
      "customer_email": "bill.john@mekari.com",
      "customer_phone": "08123123123",
      "status": "unpaid"
    }
  },
  "links": {
    "self": "https://payment-service-production.cd.jurnal.id/web/invoices/10ffb09a-2b3d-497d-a55e-60bbc3d8dddd"
  }
}
```

### URL Parameters

Parameter | Description
--------- | -----------
uuid | The Invoice ID.

### Get a Spesific Invoice Response

Parameter | Description
--------- |  -----------
uuid | `string` The invoice ID.
external_id | `string` An ID of your choice.
amount_formatted | `string` Invoice amount with formatted presentation.
description | `string` The invoice description.
due_date | `string` The invoice due date.
due_date_formatted | `string` The invoice due date with formatted persentation. The format will follows: DD/MM/YYY.
company_name | `string` The company's name who created the invoice.
customer_name | `string` The customer's name who created the invoice.
customer_email | `string` The customer's email who created the invoice.
customer_phone | `string` Phone number of customer. (e.g. 08123123123)
status | `string` The current status of invoice. 
links | `Object` Link of invoice payment page.

### Get a Spesific Invoice Error

List of posible error

> Example of get a spesific invoice error response

```json
{
  "errors": [
    {
      "code": "RecordNotFound",
      "title": "Invoice not found",
      "details": "Couldn't find Invoice"
    }
  ]
}
```

Parameter | Description
--------- | -----------
RecordNotFound | The invoice was not found in system.


## Update a Specific Invoice

The endpoint for update a spesific invoice. 

```shell
PUT /api/v2/invoices/:uuid
```

### URL Parameters

Parameter | Description
--------- | -----------
uuid | The ID of the mekari payment invoice.

### Update a Spesific Invoice Request

> Example of update a spesific invoice request

```json
{
  "external_id": "invoice-sample-production-001-updated",
  "amount": 700000,
  "description": "This is first sample invoice updated",
  "due_date": "2010-06-20",
  "company_name": "Mekari Updated",
  "customer_name": "Bill John Updated",
  "customer_email": "bill.john.updated@mekari.com",
  "customer_phone": "081231231234",
  "status": "expired"
}
```

Parameter | Description
--------- |  -----------
external_id | `string` An ID of your choice.
amount |  `number` Amount end-customer will pay. 
description | `string` The invoice description.
due_date | `string` The invoice due date.
company_name | `string` The company name who creates the invoice
customer_name | `string` The customer name who creates the invoice
customer_email | `string` The customer email who cretes the invoice. System use this field to send email when payment was received.  
customer_phone | `string` Phone number of customer. (e.g. 08123123123)
status | `string` The invoice status. <br> **Note**: Available status: *void*, *expired*, *unpaid*, *paid*. 

### Update a Spesific Invoice Response

> Example of update a spesific invoice response

```json
{
  "data": {
    "id": "10ffb09a-2b3d-497d-a55e-60bbc3d8dddd",
    "type": "invoice",
    "attributes": {
      "uuid": "10ffb09a-2b3d-497d-a55e-60bbc3d8dddd",
      "external_id": "invoice-sample-production-001-updated",
      "amount_formatted": "Rp 700.000,00",
      "description": "This is first sample invoice updated",
      "due_date": "2010-06-20T00:00:00.000Z",
      "due_date_formatted": "20/06/2010",
      "company_name": "Mekari Updated",
      "customer_name": "Bill John Updated",
      "customer_email": "bill.john.updated@mekari.com",
      "customer_phone": "081231231234",
      "status": "expired"
    }
  },
  "links": {
    "self": "https://payment-service-production.cd.jurnal.id/web/invoices/10ffb09a-2b3d-497d-a55e-60bbc3d8dddd"
  }
}
```

Parameter | Description
--------- |  -----------
uuid | `string` The invoice ID.
external_id | `string` An ID of your choice.
amount_formatted | `string` Invoice amount with formatted presentation.
description | `string` The invoice description.
due_date | `string` The invoice due date.
due_date_formatted | `string` The invoice due date with formatted persentation. The format will follows: DD/MM/YYY.
company_name | `string` The company's name who created the invoice.
customer_name | `string` The customer's name who created the invoice.
customer_email | `string` The customer's email who created the invoice.
customer_phone | `string` Phone number of customer. (e.g. 08123123123)
status | `string` The current status of invoice. 
links | `Object` Link of invoice payment page.

### Update a Spesific Invoice Error

> Example of update a spesific invoice error response

```json
{
  "errors": [
    {
      "code": "CouldNotChangeInvoiceAmount",
      "title": "Could not change invoice amount",
      "details": "Invoice amount could not be changed because the invoice has already have virtual accounts, please generate the new invoice"
    }
  ]
}
```

List of posible error

Name | Description
--------- |  -----------
CouldNotChangeInvoiceAmount | Invoice amount could not be changed because the invoice has already have virtual accounts, please generate the new invoice
CouldNotChangeInvoiceStatus | Invoice status should in list of *void*, *expired*, *unpaid*, *paid*.


