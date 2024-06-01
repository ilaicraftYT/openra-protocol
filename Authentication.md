# AuthID signing

Key is a `RSA` key.

Server verifies AuthID/`AuthToken` as it follows:
1. Server sends 256 bytes generated pseudorandomly.
2. Client signs those 256 bytes with its private key.
3. Client sends back the signed 256 bytes.
4. Server will get user's public key from the public-key database.
5. Server will verify the signature (decipher) with the public-key database.
6. If the original bytes and the signed ones match, the user is authenticated.

(Process by @rivestoss, unverified as of now)
`Fingerprint` usage in `0xFE` order back from client unknown.

# Server Password Authentication

>[!IMPORTANT]
>TODO! Please help :)
>It requires a whole section here anyways?


