Through this document you might find different types. It mostly follows the standard, so "follow your heart". Anyways, here's a table if you have any doubt.

>[!IMPORTANT]
>If there's a type specified somewhere that it isn't here, please open a issue.


OpenRA's byte order (from what I've tested) is `LittleEndian`

| Name     | Size (bytes) | Range                     | Notes                                                                                                                            |
| -------- | ------------ | ------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `byte`   | 1            | 0 to 255                  |                                                                                                                                  |
| `bool`   | 1            | 0 or 1                    | Byte treated as boolean, 0 is false, anything greater is true.                                                                   |
| `short`  | 2            | -32768 to 32767           |                                                                                                                                  |
| `ushort` | 2            | 0 to 65535                |                                                                                                                                  |
| `int`    | 4            | -2147483648 to 2147483647 | Signed 32-bit integer                                                                                                            |
| `uint`   | 4            | 0 to 2955                 | Unsigned 32-bit integer                                                                                                          |
| `long`   | 8            | -2^63 to 2^63-1           | Signed 64-bit integer                                                                                                            |
| `ulong`  | 8            | 2^64-1                    | Unsigned 64-bit integer                                                                                                          |
| `float`  | 4            |                           | A [single-precision 32-bit IEEE 754 Floating point number](https://en.wikipedia.org/wiki/Single-precision_floating-point_format) |
| `long`   | 8            |                           | A [double-precision 64-bit IEEE 754 Floating point number](https://en.wikipedia.org/wiki/Single-precision_floating-point_format) |
| `string` |              |                           | Same data structure as if it were a ByteArray, but it contains textual data.                                                     |

An indication of *Serverbound* or *Clientbound* means the direction it's going in, into the server, or into the client, respectively.

Runtime protocol communication (Handshake, Game, Lobby) mention order types and fields' byte or short identifier, not their names.