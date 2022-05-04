# WebSocket API

The daemon listens for WebSocket connections on port 8001. That server is used
for API that requires transmitting continuos streams of data.

## Initialization

In order to initialize the WebSocket session, you first have to send a JSON
message of the following structure:

```ts
type Init = {
  corekey: string; // same as the X-Duxcore-CoreKey header
  command: CommandAttach;
};
```

## Attach

```ts
type CommandAttach = {
  type: "attach";
  data: string; // service id
};
```

The attach command starts the specified service and connects you with a tty of
the container. The messages are sent in binary blobs, because not all commands
may output valid UTF-8 data. Use the [`attach-example.js`](./attach-example.js)
script as reference client implementation.