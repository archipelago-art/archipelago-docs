---
layout: default
title: WebSocket API
nav_order: 4
has_children: true
---

# ↔️ WebSocket API

The Archipelago WebSocket server allows clients to subscribe to a feed of events for one or many `collections`. The WebSocket server is a great way to get real-time updates on the Archipelago marketplace. The connection is persistent and will remain open until the client closes it.

## Connecting to the WebSocket Server

The WebSocket server is available at `wss://ws.archipelago.art`. You can connect to the server using any WebSocket client. 

The first message sent to the server should be a [`HEARTBEAT` message](message_pairs.md#heartbeat). After that, a [`SUBSCRIBE_TOPIC` message](message_pairs.md#subscribe-topic) can be sent to subscribe to a specific `collection`.

Sample code for connecting to and interacting with the WebSocket server can be found in the [Sample Code](sample_code.md) section.

## Message Nonce

Any message that is sent to the WebSocket may include an optional `nonce` field. If specified, the server will return the `nonce` back in the response message. This can be useful for tracking the reponse to individual messages admist a large amount of traffic. An example of this can be found in the [Sample Code](sample_code.md) section.
