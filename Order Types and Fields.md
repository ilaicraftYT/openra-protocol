Order types, in this format: `0xBYTE: DESCRIPTIVE NAME (NAME IN CODE)`

* `0x65`: **World Sync Hash** (SyncHash)
	* `int` Value of the sync hash
	* `ulong` Current defeat state (1 = defeated) **\***
* `0xBF`: **Player Disconnected** (Disconnect)
	* `int` Client ID that disconnected
* `0xFE`: **Handshake** (Handshake)
	* "Also used for ServerOrders for ProtocolVersion.Orders < 8"
	* `string` Length-prefixed string specifying a name or key
	* `string` Length-prefixed string specifiying a value / data
* `0xFF`: **World Order** (Fields)
	* `string` Length-prefixed string specifying the order name
	* `byte` OrderFields enum encoded as a byte: specifies the data included in the rest of the order
	* Order-specific data, continue reading for details
* `0x10`: **Order Acknowledgement** (Ack) (*Clientbound packet only*)
	* *Clientbound only* packet in response to world orders
	* `int` Frame number that the client should apply the orders it sent
	* `byte` Containing the number of sent order packets to apply
* `0x20`: **Ping** (Ping)
	* `long` Server timestamp when the ping was generated
	* *Serverbound only:* `byte` Number of frames ready to simulate
* `0x76`: **Tick Scale** (TickScale)
	* `float` Scale

Order fields, in this format: `0xSHORT: NAME IN CODE`

* `0x0`: **None**
* `0x01`: **Target**
* `0x02`: **ExtraActors**
* `0x04`: **TargetString**
* `0x08`: **Queued**
* `0x10`: **ExtraLocation**
* `0x20`: **ExtraData**
* `0x40`: **TargetIsCell**
* `0x80`: **Subject**
* `0x100`: **Grouped**

Directly feeded from https://github.com/OpenRA/OpenRA/blob/b693f20789c96e1656a01d6877d14289b57430a7/OpenRA.Game/Network/Order.cs and https://github.com/OpenRA/OpenRA/blob/b693f20789c96e1656a01d6877d14289b57430a7/OpenRA.Game/Server/ProtocolVersion.cs

**\**** What's the reason of it being a `uint64` and not a single byte?