## Implementors Guide

### Implementations

Proof of concept implementations of `did:tdw` software for [[ref: DID Controllers]] and resolvers can be found here:

- Typescript: [https://github.com/bcgov/trustdidweb-ts](https://github.com/bcgov/trustdidweb-ts)
- Python: To be added

Both currently (as of 2024.04.11) support all of the features of `did:tdw` except for [[ref:  Key Pre-Rotation]] and [[ref: Verifiable Conditions]].

The Typescript implementation is currently less than 1000 lines of Typescript code.

### Using Pre-Rotation Keys

Best practices are that the [[ref: DID Controller]] generates the active key for the DIDDoc where it can be used for "production" purposes, and generates the "next key" in an isolated location from production

::: todo

Complete this section, covering guidance on where to hold pre-rotation keys and post-quantum key rotations.

:::

### Moving a DID's Web Location

::: todo

Complete this section

:::