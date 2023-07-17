---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='#'>Documentation Powered by A10031</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Welcome to the Indico Documentation API
# Authentication

> To authorize, use this code:


```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "x-api-key: api-key-xxxx"
```

> Make sure to replace `api-key-xxxx` with your API key.

The API Using some credentials, please contact INDICO Tech Team on it !

`x-api-key: api-key-xxxx`

<aside class="notice">
You must replace <code>api-key-xxxx</code> with your personal API key.
</aside>

# coda

## List SKU


```shell
curl "http://example.com/coda/v1" \
  -H "x-api-key: api-key-xxxx"
```

> Example Request

```json
{
  "game_name":"steam-voucher",
  "service_name":2
}
```

> Example Response

```json
{
  "id": "a138713e-04a0-4e63-9e52-51ed4343709f",
  "jsonrpc": "2.0",
  "result": {

    "skuList": [
      {
        "description": "Steam Wallet Code IDR1xxxx",
        "price": {
          "amount": 12700,
          "currency": "IDR"
        },
        "sku": "STEAMIDR1xxxx"
      }
    ]
  }
}
```

This endpoint retrieves list sku

### HTTP Request

`POST http://example.com/coda/v1`

### Request Body

Parameter | Required | Description
--------- |----------| -----------
game_name | true     | the completed name listed on coda sandbox
service_name | true     | `0.place order` `1.Get Order` `2.list SKU`

<aside class="success">
Remember — List SKU authenticated by AWS Api Key
</aside>

## Voucher - Place Order


```shell
curl "http://example.com/coda/v1" \
  -H "x-api-key: api-key-xxxx"
```

> Example Request

```json
{
  "game_name": "steam-voucher",
  "sku": "SKU10001",
  "amount": 1000,
  "service_name": 0
}
```

> Example Response

```json
{
  "id": "a138713e-04a0-4e63-9e52-51ed4343709f",
  "jsonrpc": "2.0",
  "result": {
    "status": "FULFILLED",
    "orderId": "1c6cda00-375c-476e-8e1f-6b59ec958632",
    "items": [
      {
        "sku": "SAMPLE-SKU-0U36C",
        "codes": "test1IDR12k-00495"
      }
    ]
  }
}
```

This endpoint to purchase the voucher code by sku

### HTTP Request

`POST http://example.com/coda/v1`

### Request Body

Parameter | Required | Description
--------- |----------| -----------
game_name | true     | the completed name listed on coda sandbox
sku | true     | provided by coda and available on the List SKU API result
amount | true | dependent with sku value
service_name | true     | `0.place order` `1.Get Order` `2.list SKU`

<aside class="success">
Remember — Get Order authenticated by AWS Api Key
</aside>

## Voucher - Get Order


```shell
curl "http://example.com/coda/v1" \
  -H "x-api-key: api-key-xxxx"
```

> Example Request

```json
{
  "game_name": "steam-voucher",
  "order_id": "r5fga156538iKli688",
  "service_name": 1
}
```

> Example Response

```json
{
  "id": "a138713e-04a0-4e63-9e52-51ed4343709f",
  "jsonrpc": "2.0",
  "result": {
    "status": "FULFILLED",
    "orderId": "1c6cda00-375c-476e-8e1f-6b59ec958632",
    "voucher": [
      {
        "sku": "SAMPLE-SKU-0U36C",
        "codes": "test1IDR12k-00495"
      }
    ]
  }
}
```

This endpoint to get order detail by orderID

### HTTP Request

`POST http://example.com/coda/v1`

### Request Body

Parameter | Required | Description
--------- |----------| -----------
game_name | true     | the completed name listed on coda sandbox
order_id | true     | provided by coda on Place Order API Result
service_name | true     | `0.place order` `1.Get Order` `2.list SKU`

<aside class="success">
Remember — Get Order authenticated by AWS Api Key
</aside>

