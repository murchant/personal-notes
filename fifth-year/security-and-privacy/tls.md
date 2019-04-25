## TLS 1.2

### TLS
- **TLS** = Transport Layer Security. Cryptographic protocol designed for secure communication across web.
- **TLS** is the *Best Current Practise (BCP)* used.

### HSTS
- **HSTS:** HTTP Strict Transport Security.
- Allows web servers to declare that browsers should interact with them only using using only **HTTPS** connections.
  - Stephen: *"Allows a web site to say that 'you better use TLS for me (and these subdomains) for the next <many> seconds'"*
- Application should do something like *HSTS*, but don't.
- Work to define that for mail transport/IMAP under way still.
- *HTTP* clients/servers MUST support.
- *HTTP* servers SHOULD use.
- **(RFC 6797)**

## Compression
- **BEAST** & **CRIME** attack show content of web cookies can be recovered when data compression is used along with **TLS**.
- **Do not use compression**. Must not be supported
- Some applications are fine but better to do at application layer.

## Session
#### (Resumption/Renegotiation)
- Session tickets must be as good as Cipher.
- Tickets must be regularly changed (eg: Weekly). (RFC 5077).
- TLS renegotiation – MUST implement
renegotiation_info extension/hack (RFC 5746)
- Hack discovered where hacker can splice their own requests into the beginning conversation between Client and Server.

## SNI Server Name Indication
- SNI must be supported (RFC 6066).
- Explanation
  - TLS Handshake happens before application layer start.
  - Name based virtual servers share same certificate as their server has to send certificate during handshake.
  - **Solution:** Add virtual server host name in *"subjectAltName extension"*.
  - **Implementation:** Transport Layer Security (TLS) Extensions allow clients to include a Server Name Indication extension (SNI) in the extended ClientHello (handshake) message.
  - This extension hints the server immediately which name the client wishes to connect to, so the server can select the appropriate certificate to send to the clients.
  - **Stephen:** but use of **SNI** is a "'local matter'".
  - SNI has privacy implications – TLSv1.2 does not provide confidentiality for handshake extensions like SNI.

## ALPN
#### Application Layer Protocol Negotiation
- ALPN (RFC 7301) is a TLS extension that allows a
client and server to agree on which application layer protocol
(primarily HTTP/1.2 or h2) they want to use
- Sent in clear in TLSv1.2, NPN was an equivalent proposal
that saw some initital use and was encrypted, but somewhat
problematic

## Ciphersuite Guidelines
| Should Not | Must Not | Must support |
|-----------|----------| --------|
| RSA Key Transport| NULL encryption| Forward Secrecy|
| <128 bits of “strength” | RC4      |                      |
| | <112 bits of “strength” |

## Lengths/Strengths
## 7525 Misc. Stuff
## TLS Measurement
