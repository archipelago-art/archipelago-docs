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

### Market Routes
- [GET `/market/views`](market_routes.md#get-marketviews)
- [GET `/market/volume`](market_routes.md#get-marketvolume)

## Route Table

| HTTP Method(s) | Resource                                            |
| :------------- | :-------------------------------------------------- |
| `GET`          | [`/market/views`](market_routes.md#get-marketviews) |
| `GET`          | `/market/volume`                                    |
| `GET`          | `/market/floor-asks`                                |
| `GET`          | `/market/asks/:askId`                               |
| `POST`         | `/market/orders`                                    |
| `GET`          | `/market/collection`                                |
| `GET`          | `/market/collection/:slug`                          |
| `GET`          | `/market/collection/:slug/features`                 |
| `GET`          | `/market/collection/:slug/asks`                     |
| `GET`          | `/market/collection/:slug/bids`                     |
| `GET`          | `/market/collection/:slug/last-sales`               |
| `GET`          | `/market/collection/:slug/events`                   |

