## Abstract

The `did:tdw` (Trust DID Web) method is an enhancement to the
`did:web` protocol, providing a complementary web-based DID method that addresses limitations
of `did:web`. It's features include the following.

- Ongoing publishing of all DID Document (DIDDoc) versions for a DID instead of,
  or alongside a `did:web` DID/DIDDoc.
- Uses the same DID-to-HTTPS transformation as `did:web`.
- Provides resolvers the full history of the DID using a verifiable chain of
  updates to the DIDDoc from genesis to deactivation.
- A [[def: self-certifying identifier]] (SCID) for the DID that is globally
  unique and derived from the initial DIDDoc that enables DID portability, such
  as moving the DIDs web location (and so the DID string itself) while retaining
  the DID's history.
- DIDDoc updates include a proof signed by the DID Controller(s) *authorized* to
  update the DID.
- An optional mechanism for publishing "pre-rotation" keys to prevent loss of
  control of the DID in cases where an active private key is compromised.
- DID URL path handling that defaults (but can be overriden) to automatically
  resolving `<did>/path/to/file` by using a comparable DID-to-HTTPS translation
  as for the DIDDoc.
- A DID URL path `<did>/whois` that defaults to automatically returning (if
  published by the DID controller) a [[ref: Verifiable Presentation]] containing
  [[ref: Verifiable Credentials]] with the DID as the `credentialSubject`,
  signed by the DID.

Combined, the additional feature enable greater trust and security without
compromising the simplicity of `did:web`. The incorporation of the DID Core
compatible "/whois" path, drawing inspiration from the traditional WHOIS
protocol [[spec:rfc3912]], offers an easy to use, decentralized, trust registry.
This `did:tdw` aims to establish a more trusted and secure web environment by
providing robust verification processes and enabling transparency and
authenticity in the management of decentralized digital identities.
