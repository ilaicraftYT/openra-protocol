Handshake begins when a client opens a connection.

`C->S`: Client to Server
`S->C`: Server to Client
`C`: Client Side Action
`S`: Server Side Action

1. **S->C**
	* `int` Specifies handshake protocol version
	* `int` Specifies new connection's client ID
	* **This packet ignores default packet structure**
2. **S->C**
	* `0xFE` order
	* `string` Encodes a `HandshakeRequest` yaml blob containing at least: **\***
		* `Mod` Internal ID for the mod
		* `Version` Internal version string for the active mod
		* `AuthToken` Blob of random data that the client can sign to verify their AuthID (see Authentication.md for details)
3. **C**: Disconnects and shows a mod switch dialog if either Mod or Version don't match
4. **C->S**
	* `0xFE` order
	* `string` Encodes a `HandshakeResponse` yaml blob contaning at least:
		* `Mod` Internal ID for the mod
		* `Version` Internal version string for the active mod
		* `Client`
			* `Name` Client name
			* *optional* `PreferredColor` Client's preferred color
			* *optional* `Password` Password to enter the server
		* `Fingerprint` String used to query the players authentication public key (see Authentication.md for details)
		* `AuthSignature` AuthToken signature generated using the client's authentication public key
		* `OrdersProtocol` *ProtocolVersion.Orders* that the client will use (7 if omitted)
5. **S**: Disconnect client if Mod or Version don't match or it does not accept the requested OrderProtocol
6. **S:** Server checks password and sends an `AuthenticationError` yaml blob/order (?) then disconnects **#**

**\*** I have observed that the yaml blob title is `HandshakeRequestHandshake` instead (see plaintext wireshark dump):
```
±³ üÑI¬ËEè@@'c®øíÀ¨d ÓR¥Ð á_ÊêùB
¼¼µ¬þHandshakeRequestHandshake:
  Mod: ra
  Version: release-20231010
  AuthToken: *****
```

**#** Client actually tries to connect without any password then server returns error and only then actually requests user for input. Even though documentation says that it's a order, it's actually a kinda yaml-like `<key>:<value>` string. See Authentication.md for details.