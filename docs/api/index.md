---
layout: default
title: REST API
nav_order: 3
has_children: true
has_toc: false
---

# 🗒️ REST API

## Table of contents
{: .no_toc .text-delta }
- TOC
{:toc}

---

## Base Path

The API base path is: `https://api.archipelago.art/v1`

Currently `v1` is the latest and only version, but as new versions are released this will be updated.

**Note:** All requests must be made over HTTPS.

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
- [`/market/views`](market_routes.md#get-marketviews)
- [`/market/volume`](market_routes.md#get-marketvolume)

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

