---
layout: default
title: REST API
nav_order: 3
has_children: true
has_toc: false
---

# 🗒️ REST API
{: .no_toc }

The Archipelago REST API is a set of endpoints that allow you to interact with the Archipelago marketplace. You can use the REST API to retrieve information about the marketplace, collections, and items, as well as place orders.

## Table of contents
{: .no_toc .text-delta }
- TOC
{: toc }

---

## Base Path

The API base path is: `https://api.archipelago.art/v1`

Currently `v1` is the latest and only version, but as new versions are released this will be updated.

**Note:** All requests must be made over HTTPS.

### Example Request
Paste the following into your terminal to make your first request. This example returns the details of a specific token (NFT).

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/subscapes/99
```

## Resource Hierarchy

The overall hierarchy of the Archipelago API is structured as follows:

```
|-- https://api.archipelago.art/v1/
|  |-- user
|  |-- market
|  |  |-- orders
|  |  |-- collections
|  |  |  |-- tokens
```

## Full Route List

### User Routes

- [POST `/user/login`](user_routes.md#post-userlogin)
- [POST `/user/set-email`](user_routes.md#post-userset-email)
- [GET `/user/info`](user_routes.md#get-userinfo)
- [GET `/user/bids`](user_routes.md#get-userbids)
- [GET `/user/asks`](user_routes.md#get-userasks)
- [GET `/user/:account/tokens`](user_routes.md#get-useraccounttokens)

### Market Routes

- [GET `/market/views`](market_routes.md#get-marketviews)
- [GET `/market/volume`](market_routes.md#get-marketvolume)
- [GET `/market/floor-asks`](market_routes.md#get-marketfloor-asks)
- [GET `/market/floor-bids`](market_routes.md#get-marketfloor-bids)
- [GET `/market/asks/:askId`](market_routes.md#get-marketasksaskid)
- [GET `/market/bids/:bidId`](market_routes.md#get-marketbidsbidid)

### Order Routes

- [POST `/market/orders`](order_routes.md#post-marketorders)
  
### Collection Routes

- [GET `/market/collections/`](collection_routes.md#get-marketcollections)
- [GET `/market/collections/:slug`](collection_routes.md#get-marketcollectionsslug)
- [GET `/market/collections/:slug/features`](collection_routes.md#get-marketcollectionsslugfeatures)
- [GET `/market/collections/:slug/asks`](collection_routes.md#get-marketcollectionsslugasks)
- [GET `/market/collections/:slug/bids`](collection_routes.md#get-marketcollectionsslugbids)
- [GET `/market/collections/:slug/last-sales`](collection_routes.md#get-marketcollectionssluglast-sales)
- [GET `/market/collections/:slug/events`](collection_routes.md#get-marketcollectionsslugevents)

### Token Routes

- [GET `/market/collections/:slug/:tokenIndex`](token_routes.md#get-marketcollectionsslugtokenindex)
- [GET `/market/collections/:slug/:tokenIndex/features`](token_routes.md#get-marketcollectionsslugtokenindexfeatures)
- [GET `/market/collections/:slug/:tokenIndex/history`](token_routes.md#get-marketcollectionsslugtokenindexhistory)
- [GET `/market/collections/:slug/:tokenIndex/ask`](token_routes.md#get-marketcollectionsslugtokenindexask)
- [GET `/market/collections/:slug/:tokenIndex/orders`](token_routes.md#get-marketcollectionsslugtokenindexorders)
