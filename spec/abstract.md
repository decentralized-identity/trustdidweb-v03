## Abstract

The evolution of Decentralized Identifiers (DIDs) continues to be a dynamic area of development in the quest for secure and private digital identity management. The `did:web` method, praised for its simplicity and ease of deployment, allows for DIDs to be associated with a domain's reputation or published on platforms like GitHub. However, it is not without its challenges, particularly concerning security vulnerabilities inherited from the web and the absence of a verifiable history for the DID. Addressing these concerns, the proposed `did:tdw` (Trust DID Web) method aims to enhance the `did:web` by introducing a verifiable history feature, akin to what is available with ledger-based DIDs, but crucially, without relying on a ledger. This approach not only maintains backward compatibility but also offers an additional layer of assurance for those requiring more robust verification processes. By publishing the resulting DID as both `did:web` and `did:tdw`, it caters to a broader range of trust requirements, from those who are comfortable with the existing `did:web` infrastructure to those seeking greater security assurances provided by `did:tdw`. This innovative step represents a significant stride towards a more trusted and secure web, where the integrity of cryptographic key publishing is paramount.

The key differences between `did:web` and `did:tdw` revolve around the core issues of decentralization and security. `did:web` is recognized for its simplicity and cost-effectiveness, allowing for easy establishment of a credential ecosystem. However, it is not inherently decentralized as it relies on DNS domain names, which require centralized registries, and it lacks a cryptographically verifiable, tamper-resistant, and persistently stored DID document. In contrast, `did:tdw` (Trust DID Web) is proposed as an enhancement to `did:web`, aiming to address these limitations by adding a verifiable history to the DID without the need for a ledger. This method seeks to provide a more decentralized approach by ensuring that the security of the embedded self-certifying identifier does not depend on DNS. Additionally, `did:tdw` offers a cryptographically verifiable trust registry and status lists, using DID-Linked Resources, which `did:web` lacks. These features are designed to build a trusted web, offering a higher level of assurance for cryptographic key publishing and management.

For backwards compatibility, and for verifiers that just "trust" `did:web`, a `did:tdw` can be trivially modified and published in parallel as a `did:web` DID. For resolvers that want more assurance, `did:tdw` provides a way to "trust did:web" (or to enable a "trusted web" if you say it fast), by supporting these features:

- Ongoing publishing of all DID Document (DIDDoc) versions for a DID instead of, or beside, a `did:web` DID.
- Uses the same DID-to-HTTPS transformations as `did:web`.
- Provides resolvers the full history of the DID using a verifiable chain of
  updates to the DIDDoc from creation to the current update.
- A [[def: self-certifying identifier]] (SCID) for the DID that is globally unique and
  derived from the initial DIDDoc, enabling verifiable "alsoKnownAs" DIDs.
- DIDDoc updates include a proof signed by the DID Controller(s) authorized
  to update the DID.
- An optional mechanism for publishing "pre-rotation" keys to prevent loss of
  control of the DID in cases where an active private key is compromised.
- DID URL path handling that defaults to automatically resolving a
  `<did>/path/to/file` being retrieved through using a comparable DID-to-HTTPS
  translation as for the DIDDoc.
- A DID URL path `<did>/whois` that defaults to automatically returning a [[ref:
  Verifiable Presentation]] containing [[ref: Verifiable Credentials]] with the
  DID as the `credentialSubject`, signed by the DID.

The following is a `tl;dr` summary of the specification summarizing how `did:tdw` works.

- Beside where DID resolvers find `did:web`'s `did.json`, `did:tdw`'s `didlog.txt`
  file is found. The same `did:web` DID-to-HTTPS transformation is used.
- The `didlog.txt` is a list of JSON [[ref: DID log entries]], one per line,
  whitespace removed, each of which contains the information needed to derive a
  version of the DIDDoc from its preceding version.
- Each entry includes six JSON entries:
  1. A hash of the entry.
  2. The `versionId` of the DIDDoc, starting from 1 and incrementing.
  3. The `versionTime` (as stated by the DID Controller) of the entry.
  4. A set of `parameters` that impact the processing of the current and
    future log entries.
       - Example parameters are the version of the `did:tdw` specification
      and hash algorithm being used.
  5. The new version of the DIDDoc as either a `value` (the full document) or a
    `patch` derived using [[ref: JSON Patch]] to update the new version from the
    previous entry.
  6. A [[ref: Data Integrity]] (DI) proof across the entry, signed by a DID
    Controller authorized to update the DIDDoc.
- In generating the first version of the DIDDoc, the DID Controller calculates
  the [[ref: SCID]] for the DID, includes it as a `parameter` in the first log entry, and
  inserts it where needed in the initial (and all subsequent) DIDDocs.
- A DID Controller generates and publishes the updated log file by making it available at the appropriate
  location on the web, based on the value of the DID.
- Given a `did:tdw` DID, a resolver converts the DID to an HTTPS URL, retrieves, and processes the
  log file `didlog.txt`, generating and verifying each log entry as per the requirements outlined
  in this specification.
  - In the process, the resolvers may collect all the DIDDoc versions and public
    keys (by reference) used by the DID currently, or in the past. This enables resolving both current and past DID URLs.
- Optionally, a DID Controller could generate and publish a `did:web` DIDDoc from
  the latest `did:tdw` DIDDoc by changing the `id` to the `did:web` DID, and
  adding an `alsoKnownAs` for the `did:tdw` (indicating to a resolver that they
  can verify the DIDDoc, if wanted).
  - Of course, a resolver settling for just the `did:web` version of the DID
    does not get the verifiability of the `did:tdw` log.
- `did:tdw` DID URLs with paths and `/whois` are resolved to documents published by the
  DID Controller by default in the web location relative to the `didlog.txt` file.

An example of a `did:tdw` evolving through a series of versions can be seen in
the [did:tdw Examples](#didtdw-example) of this specification.
