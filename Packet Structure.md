OpenRA has a basic packet structure:

| Name     | Type    | Description                                                                                                   |
| -------- | ------- | ------------------------------------------------------------------------------------------------------------- |
| Length   | `int32` | Defines packet length, server should close connection if a packet larger than `128kB` is received.            |
| ClientId | `int32` | The client id that is sending the orders, `0` if it's from server.                                            |
| Frame    | `int32` | Specifies the game network tick (or "frame") the order belongs to.                                            |
| Order    | `*`     | Zero or more orders, encoded as byte order data or order-specific data. See order types for more information. |
