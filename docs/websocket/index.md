---
layout: default
title: WebSocket API
nav_order: 4
has_children: true
---

# ↔️ WebSocket API

It's also possible to communicate with the Archipelago API via a WebSocket connection. WebSockets are best suited for clients and applications that need real-time data. The Archipelago WebSocket server allows clients to subscribe to a feed of events for one or many `collections`.

## Message Nonce

Any message that you send may include an optional `nonce` field. If specified, the server will return it back to you in the response message. This can be useful if you want to track the reponse to individual messages admist a large amount of traffic. An example of this can be found in the sample code below.
