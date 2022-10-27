# Sample WebSocket Code

The code below provides a simplified example of how to connect to the Archipelago WebSocket API to send and receive your first messages.

The sample code below is written in [vanilla JavaScript](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications) designed to run in the browser.

```javascript
// Define the WebSocket and open the connection
let socket = new WebSocket("wss://api.archipelago.art/ws");

// Handle the connection open event
socket.onopen = function (event) {
  console.log("Connection to Archipelago WS established.");

  // Send an initial heartbeat message
  var heartbeat_msg = { type: "HEARTBEAT" };
  socket.send(JSON.stringify(heartbeat_msg));

  // Subscribe to receive events for a collection
  var subscribe_msg = {
    nonce: Date.now(),
    type: "SUBSCRIBE_TOPIC",
    topic: "ringers",
  };
  socket.send(JSON.stringify(subscribe_msg));
};

// Listen for messages back from the Archipelago API
socket.onmessage = function (event) {
  console.log(`Data received from Archipelago WS: ${event.data}`);
};

// Handle any errors
socket.onerror = function (error) {
  console.error(`Error ${error.message}`);
};

// Handle closing the connection
socket.onclose = function (event) {
  if (event.wasClean) {
    console.log(
      `Connection closed cleanly, code=${event.code} reason=${event.reason}`
    );
  } else {
    // e.g. server process killed or network down
    // event.code is usually 1006 in this case
    console.error(`Connection died, code=${event.code}`);
  }
};
```

### Sample Output

Running the sample code above should yield the output below:

```
Connection to Archipelago WS established.
Data received from Archipelago WS: {"type":"HEARTBEAT_RESPONSE","data":{"time":1655056473},"status":200}
Data received from Archipelago WS: {"type":"ADD_TOPIC","data":{"topics":["ringers"]},"status":200,"nonce":1655069434775}
```
