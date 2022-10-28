---
layout: default
title: REST API
nav_order: 3
has_children: true
---

# 🗒️ REST API

## Base Path

The API base path is: `https://api.archipelago.art/:version`

Currently `v1` is the latest and only version, so all API calls should be made to `https://api.archipelago.art/v1`


All requests must be made over HTTPS.
{: .info }

## Resource Hierarchy

The overall hierarchy of the Archipelago API is structured as follows:

```
https://api.archipelago.art/v1
|  /market
|  |- /collections
|  |- /orders
|  /user
```

## Resource List

| HTTP Method(s) | Resource                              | Link                                     |
| :------------- | :------------------------------------ | :--------------------------------------- |
| `GET`          | `/market/views`                       | [Docs](market_routes.md#get-marketviews) |
| `GET`          | `/market/volume`                      | [Docs](market_routes.md#get-marketviews) |
| `GET`          | `/market/floor-asks`                  | [Docs](market_routes.md#get-marketviews) |
| `GET`          | `/market/asks/:askId`                 | [Docs](market_routes.md#get-marketviews) |
| `POST`         | `/market/orders`                      | [Docs](market_routes.md#get-marketviews) |
| `GET`          | `/market/collection`                  | [Docs](market_routes.md#get-marketviews) |
| `GET`          | `/market/collection/:slug`            | [Docs](market_routes.md#get-marketviews) |
| `GET`          | `/market/collection/:slug/features`   | [Docs](market_routes.md#get-marketviews) |
| `GET`          | `/market/collection/:slug/asks`       | [Docs](market_routes.md#get-marketviews) |
| `GET`          | `/market/collection/:slug/bids`       | [Docs](market_routes.md#get-marketviews) |
| `GET`          | `/market/collection/:slug/last-sales` | [Docs](market_routes.md#get-marketviews) |
| `GET`          | `/market/collection/:slug/events`     | [Docs](market_routes.md#get-marketviews) |

