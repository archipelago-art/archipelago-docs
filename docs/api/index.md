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

## Resource Hierarchy

The overall hierarchy of the Archipelago API is structured as follows:

```
https://api.archipelago.art/v1
|  /market
|  |- /collections
|  |- /orders
|  /user
```
