## Abstract

`did:web` a useful, simple DID Method that makes deployment easy, and can be
used to build beautifully on a domain's existing reputation -- or even be
published content publishing platforms such as GitHub. But `did:web` also
inherits some of the security flaws of the Web and lacks a specified way to access the
history of the DID--features that created the initial excitement around
ledger-based DIDs. For something as important as cryptographic key publishing,
those missing features can be a problem.

We propose a new DID Method that compliments `did:web` that, with a relatively
simple set of dependencies and processing steps, adds a fully verifiable history
to a web-based DID such as one might get from a ledger-based DID, but without
the ledger. For backwards compatibility, and for verifiers that just "trust"
`did:web`, the resulting DID can be published as a `did:web` in parallel. For
resolvers that want more assurance, `did:tdw` (Trust DID Web) provides a way to
"trust did:web" (or to enable a "trusted web" if you say it fast), by supporting
these features:

- Publishing of all DIDDoc versions for a DID instead of, or beside, a `did:web` DID.
- Uses the same DID-to-HTTPS transformations as `did:web`.
- Provides resolvers with the full history of the DID via a verifiable chain of
  updates to the DIDDoc from creation to the latest update.
- A [[def: self-certifying identifier]] (SCID) for the DID that is globally unique and
  derived from the initial DIDDoc, enabling verifiable "alsoKnownAs" DIDs.
- Each DIDDoc update includes a proof signed by the DID Controller(s) authorized
  to update the DID.
- An optional mechanism for publishing "pre-rotation" keys to prevent loss of
  control of the DID in cases where an active private key is compromised.
- A DID Method-specific (but useful for other DID Methods) approach to
  publishing documents (files, verifiable credentials, verifiable presentations,
  etc.) via the DID URL path. For example, a company can publish a verifiable
  credential rendering package as a JWS signed by the issuer's DID and at the
  URL `<did>/path/to/render_credential.jws`.

The following is a `tl;dr` summary of the specification summarizing how `did:tdw` works.

- Beside where DID resolvers find `did:web`'s `did.json`, `did:tdw`'s `didlog.txt`
  file is found. The same `did:web` DID-to-HTTPS transformation is used.
- The `didlog.txt` is a list of JSON [[ref: DID log entries]], one per line,
  whitespace removed, each of which contains the information needed to derive a
  version of the DIDDoc from its preceding version.
- Each entry includes JSON entries containing:
  - A hash of the entry.
  - The `versionId` of the DIDDoc, starting from 1 and incrementing.
  - The `versionTime` (as stated by the DID Controller) of the entry.
  - A set of `parameters` that impact the processing of the current and
    future log entries.
    - Examples parameters are the version of the `did:tdw` specification
      and the hash algorithm being used by the controller. All available parameters are
      defined in this specification.
  - The new version of the DIDDoc as either a `value` (the full document) or a
    `patch` derived using [[ref: JSON Patch]] to update the new version from the
    previous entry.
  - A [[ref: Data Integrity]] (DI) proof across the entry, signed by a DID
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
- `did:tdw` DID URLs with paths can be resolved to documents published by the
  DID Controller.

An example of a `did:tdw` evolving through a series of versions can be seen in
the [did:tdw Examples](#didtdw-example) of this specification.
