---
layout: default
title: Message Pairs
parent: WebSocket API
nav_order: 1
---

# ✉️ Message Pairs
{: .no_toc }

These are the pairs of message that you (as the client) will send and receive when establishing a connection to the Archipelago WebSocket and subscribing to different topics.

## Table of Contents
{: .no_toc .text-delta }
- TOC
{:toc }

---

## Heartbeat

### Example Request
{: .no_toc }

```json
{
  "type": "HEARTBEAT"
}
```

### Example Response
{: .no_toc }

```json
{
  "type": "HEARTBEAT_RESPONSE",
  "data": {
    "time": 1655056473
  },
  "status": 200
}
```

## Subscribe Topic

### Example Request
{: .no_toc }

```json
{
  "type": "SUBSCRIBE_TOPIC",
  "topic": "ringers"
}
```

### Example Response
{: .no_toc }

```json
{
  "type": "ADD_TOPIC",
  "data": {
    "topics": ["ringers"]
  },
  "status": 200
}
```

## Unsubscribe Topic

### Example Request
{: .no_toc }

```json
{
  "type": "UNSUBSCRIBE_TOPIC",
  "topic": "ringers"
}
```

### Example Response
{: .no_toc }

```json
{
  "type": "REMOVE_TOPIC",
  "data": {
    "topics": []
  },
  "status": 200
}
```
