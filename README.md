
# The "tor-relay" Well-Known Resource Identifier

This resource identifier is used for the the verification of [Tor](https://www.torproject.org/) relay contact information 
(more specifically the [operatorurl](https://nusenu.github.io/ContactInfo-Information-Sharing-Specification/#operatorurl)).
It can also be used for autodiscovery of Tor relays run by a given entity.
It solves the issue that Tor relay contact information is an unidirectional and unverified claim by nature.
This well-knwon URI aims to allow the verification of the unidirectional claim.
It aims to reduce the risk of impersonation attacks, where a Tor relay claims to be operated by a certain entity, but actually isn't.

* An initially (unverified) Tor relay contact information might claim to be related to an
organization by pointing to its website: Tor relay contact information field -> website
* The "tor-relay" URI allows for the verification of that claim by fetching the files containing Tor relay ID(s) under the specified URI, 
because attackers can not easily place these files at the given location.

* By publishing Tor relay IDs under this URI the website operator claims to operate these relays.
The verification of listed Tor relay IDs only succeeds if the claim can be verified bidirectionally (website -> relay and relay -> website).

* This URI is not related to Tor bridges or Tor onion services.

* The URL MUST be HTTPS and use a valid TLS certificate from a generally trusted root CA. Plain HTTP MUST not be used.

* The URL MUST be accessible by robots (no CAPTCHAs).

## /.well-known/tor-relay/rsa-fingerprint.txt

* The file contains one or more Tor relay RSA SHA1 fingerprints operated by the entity in control of this website.
* Each line contains one fingerprint.
* Non-comment lines must be exactly 40 characters long and consist of the following characters [a-fA-F0-9].
* Fingerprints are not case-sensitive.
* Each fingerprint MUST appear at most once.
* The file may contain comments (starting with #).
* The file must not be larger than one MByte.
* The file MUST NOT contain fingerprints of Tor bridges (or hashes of bridge fingerprints).
* The content MUST be a media type of "text/plain".

Example file content:

```
# we operate these Tor relays
A234567890123456789012345678901234567ABC
B234567890123456789012345678901234567890
```
The RSA SHA1 relay fingerprint can be found in the file named "fingerprint" located in the Tor data directory on the relay.

## /.well-known/tor-relay/ed25519-pubkey.txt

* In addition to RSA1024 identity keys, Tor relays have Ed25519 identity keys.
* The file contains one or more Tor relay Ed25519 public keys operated by the entity in control of this website.
* Each line contains one fingerprint.
* This file contains the public Ed25519 master key in base64 encoded format.
* Non-comment lines must be exactly 43 characters long and only consist of the following characters [a-zA-Z0-9/+] (no padding "=").
* The content MUST be a media type of "text/plain".

Example file content:
```
# we operate these Tor relays
11234jWVlTPtfiwVp11234qct5cHPIcNdKBK//Db274
2z1zAVrLV4E/wEQvfV2gbb9kLtqBGsBEpNQ3d826kwA
```

# Change Controller

tor-relay-well-known-uri AT riseup.net

# Related information

* https://gitweb.torproject.org/torspec.git/tree/tor-spec.txt
* https://gitweb.torproject.org/torspec.git/tree/cert-spec.txt
* https://gitweb.torproject.org/torspec.git/tree/proposals/220-ecc-id-keys.txt
* https://nusenu.github.io/ContactInfo-Information-Sharing-Specification/#operatorurl






