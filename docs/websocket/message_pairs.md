# Message Pairs

These are the pairs of message that you (as the client) will send and receive when establishing a connection to the Archipelago WebSocket and subscribing to different topics.

## Heartbeat

### Example Request

```json
{
  "type": "HEARTBEAT"
}
```

### Example Response

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

```json
{
  "type": "SUBSCRIBE_TOPIC",
  "topic": "ringers"
}
```

### Example Response

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

```json
{
  "type": "UNSUBSCRIBE_TOPIC",
  "topic": "ringers"
}
```

### Example Response

```json
{
  "type": "REMOVE_TOPIC",
  "data": {
    "topics": []
  },
  "status": 200
}
```
