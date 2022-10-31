---
layout: default
title: Overview
nav_order: 1
---

# 🏡 Overview

This site serves as documentation for the [Archipelago Art](https://archipelago.art/) APIs. You can either navigate using the sidebar on the left, or by using the search functionality in the search box above.

The Archipelago APIs allow you to interact with the Archipelago marketplace. You can use the APIs to:
- Retrieve statistics about the marketplace (e.g. volume, views, etc.)
- Lookup market-related information for collections and tokens (e.g. floor price, last sale, bids, etc.)
- Execute market orders (e.g. buy and sell tokens) 
  - 🚧 **Note:** More information and client libraries for executing orders will be released soon.
- Get detailed information about a specific collection or token (e.g. name, description, image, features, etc.)
- Retreive information about your own bids and asks
- Lookup a user's collection of tokens
- Subscribe to events on the marketplace (e.g. new orders, new bids, etc.)

## REST API

The REST API is the primary way to interact with the Archipelago Art platform. It is a RESTful API that uses JSON for serialization.

- The detailed docs for each endpoint can be found in the [REST API](api/index.md) section
- Information on how to authenticate with the API can be found in the [Authentication](authentication.md) section
- Error codes and messages can be found in the [Errors](errors.md) section

## WebSocket API

The WebSocket API is a way to subscribe to events that occur on the Archipelago Art platform. It is a WebSocket API that uses JSON for serialization.

Detailed docs on how to use the WebSocket API can be found in the [WebSocket API](websocket/index.md) section.
