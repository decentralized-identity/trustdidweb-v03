## `did:tdw` Example

The following shows the evolution of a `did:tdw` from inception through several
versions, showing the DID, DIDDoc, [[ref: DID Log]], and some of the
intermediate data structures.

In the following, all of the data for the [[ref: DID log entries]] are displayed
as prettified JSON for readability. In the log itself, the JSON has all
whitespace removed, and each line ends with a `CR`.

### DID Creation Data

These examples show the important structures used in the [Create (Register)](#create-register) operation for a `did:tdw` DID.

#### Input to the SCID Generation Process with Placeholders

The following JSON is an example of the input that the [[ref: DID Controller]]
constructs (however they see fit) and passes into the
[SCID Generation Process](#scid-generation-and-validation).

```json
[
  "{SCID}",
  1,
  "2024-06-13T12:06:29Z",
  {
    "method": "did:tdw:1",
    "scid": "{SCID}",
    "updateKeys": [
      "did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"
    ]
  },
  {
    "value": {
      "@context": [
        "https://www.w3.org/ns/did/v1",
        "https://w3id.org/security/multikey/v1"
      ],
      "id": "did:tdw:example.com:{SCID}",
      "controller": "did:tdw:example.com:{SCID}",
      "authentication": [
        "did:tdw:example.com:{SCID}#5b48Zj6B"
      ],
      "assertionMethod": [
        "did:tdw:example.com:{SCID}#CpsUrTh3"
      ],
      "verificationMethod": [
        {
          "id": "did:tdw:example.com:{SCID}#5b48Zj6B",
          "controller": "did:tdw:example.com:{SCID}",
          "type": "Multikey",
          "publicKeyMultibase": "z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"
        },
        {
          "id": "did:tdw:example.com:{SCID}#CpsUrTh3",
          "controller": "did:tdw:example.com:{SCID}",
          "type": "Multikey",
          "publicKeyMultibase": "z6MkuocstfAaHsJgRnQgfQdtJiECuWEMDAbQV61aCpsUrTh3"
        }
      ]
    }
  }
]
```

#### Output of the SCID Generation Process

After the SCID is generated, the literal `{SCID}` placeholders are replaced by the
generated [[ref: SCID]] value (below). This JSON is the input to the
[`entryHash` generation process](#entry-hash-generation-and-validation) -- with the
[[ref: SCID]] as the first item of the array. Once the process has run, the
resulting output hash replaces the [[ref: SCID]] as the first item in the array.

```json
[
  "c6ee1vru45p8cbt3a10ubw6pz67t",
  1,
  "2024-06-13T12:06:29Z",
  {
    "method": "did:tdw:1",
    "scid": "c6ee1vru45p8cbt3a10ubw6pz67t",
    "updateKeys": [
      "did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"
    ]
  },
  {
    "value": {
      "@context": [
        "https://www.w3.org/ns/did/v1",
        "https://w3id.org/security/multikey/v1"
      ],
      "id": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t",
      "controller": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t",
      "authentication": [
        "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#5b48Zj6B"
      ],
      "assertionMethod": [
        "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CpsUrTh3"
      ],
      "verificationMethod": [
        {
          "id": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#5b48Zj6B",
          "controller": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t",
          "type": "Multikey",
          "publicKeyMultibase": "z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"
        },
        {
          "id": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CpsUrTh3",
          "controller": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t",
          "type": "Multikey",
          "publicKeyMultibase": "z6MkuocstfAaHsJgRnQgfQdtJiECuWEMDAbQV61aCpsUrTh3"
        }
      ]
    }
  }
]
```

#### Data Integrity Proof Generation and First Log Entry

The last step in the creation of the first log entry is the generation of the data integrity proof.
One of the `did:key` DIDs in the `updateKeys` parameter **MUST** be used to generate the signature
in the proof, with the `entryHash` value used as the `challenge` item. The generated proof is
added to the JSON Line as the sixth item, and the entire array becomes the first entry in the DID Log.

The following is the JSON prettified version of the entry log file that is published
as the `did.jsonl` file. When published, all extraneous whitespace is removed, as
shown in the block below the pretty-printed version.

```json
[
  "c6ee1vru45p8cbt3a10ubw6pz67t",
  1,
  "2024-06-13T12:06:29Z",
  {
    "method": "did:tdw:1",
    "scid": "c6ee1vru45p8cbt3a10ubw6pz67t",
    "updateKeys": [
      "did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"
    ]
  },
  {
    "value": {
      "@context": [
        "https://www.w3.org/ns/did/v1",
        "https://w3id.org/security/multikey/v1"
      ],
      "id": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t",
      "controller": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t",
      "authentication": [
        "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#5b48Zj6B"
      ],
      "assertionMethod": [
        "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CpsUrTh3"
      ],
      "verificationMethod": [
        {
          "id": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#5b48Zj6B",
          "controller": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t",
          "type": "Multikey",
          "publicKeyMultibase": "z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"
        },
        {
          "id": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CpsUrTh3",
          "controller": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t",
          "type": "Multikey",
          "publicKeyMultibase": "z6MkuocstfAaHsJgRnQgfQdtJiECuWEMDAbQV61aCpsUrTh3"
        }
      ]
    }
  },
  [
    {
      "type": "DataIntegrityProof",
      "cryptosuite": "eddsa-jcs-2022",
      "verificationMethod": "did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B",
      "created": "2024-06-13T12:06:29Z",
      "proofPurpose": "authentication",
      "challenge": "3dunqt4uet42kw71e1knnd3q69mfc9j4dq6dvzqzm9mrdpg6fyh0",
      "proofValue": "z3UQwVFPxeXzb82DTaXQf9AwEst7NB22doLbZVou2CNs1fnGbX1mDNVMdrGM9868vauLSmPeGex7BzRcKaEm5xvRA"
    }
  ]
]
```

The same content "un-prettified", as it is found in the `did.jsonl` file:

```json
["c6ee1vru45p8cbt3a10ubw6pz67t",1,"2024-06-13T12:06:29Z",{"method":"did:tdw:1","scid":"c6ee1vru45p8cbt3a10ubw6pz67t","updateKeys":["did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"]},{"value":{"@context":["https://www.w3.org/ns/did/v1","https://w3id.org/security/multikey/v1"],"id":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t","controller":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t","authentication":["did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#5b48Zj6B"],"assertionMethod":["did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CpsUrTh3"],"verificationMethod":[{"id":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#5b48Zj6B","controller":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t","type":"Multikey","publicKeyMultibase":"z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"},{"id":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CpsUrTh3","controller":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t","type":"Multikey","publicKeyMultibase":"z6MkuocstfAaHsJgRnQgfQdtJiECuWEMDAbQV61aCpsUrTh3"}]}},[{"type":"DataIntegrityProof","cryptosuite":"eddsa-jcs-2022","verificationMethod":"did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B","created":"2024-06-13T12:06:29Z","proofPurpose":"authentication","challenge":"3dunqt4uet42kw71e1knnd3q69mfc9j4dq6dvzqzm9mrdpg6fyh0","proofValue":"z3UQwVFPxeXzb82DTaXQf9AwEst7NB22doLbZVou2CNs1fnGbX1mDNVMdrGM9868vauLSmPeGex7BzRcKaEm5xvRA"}]]
```

#### `did:web` Version of DIDDoc

As noted in the [publishing a parallel `did:web`
DID](#publishing-a-parallel-didweb-did) section of this specification a `did:tdw` can be published
by replacing `did:tdw` with `did:web` in the DIDDoc, adding an `alsoKnownAs` entry for the `did:tdw`
and publishing the resulting DIDDoc at `did.json`, logically beside the `did.jsonl` file.

Here is what the `did:web` DIDDoc looks like for the `did:tdw` above.

```json
{
      "@context": [
        "https://www.w3.org/ns/did/v1",
        "https://w3id.org/security/multikey/v1"
      ],
      "id": "did:web:example.com:c6ee1vru45p8cbt3a10ubw6pz67t",
      "controller": "did:web:example.com:c6ee1vru45p8cbt3a10ubw6pz67t",
      "alsoKnownAs": ["did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t"],
      "authentication": [
        "did:web:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#5b48Zj6B"
      ],
      "assertionMethod": [
        "did:web:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CpsUrTh3"
      ],
      "verificationMethod": [
        {
          "id": "did:web:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#5b48Zj6B",
          "controller": "did:web:example.com:c6ee1vru45p8cbt3a10ubw6pz67t",
          "type": "Multikey",
          "publicKeyMultibase": "z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"
        },
        {
          "id": "did:web:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CpsUrTh3",
          "controller": "did:web:example.com:c6ee1vru45p8cbt3a10ubw6pz67t",
          "type": "Multikey",
          "publicKeyMultibase": "z6MkuocstfAaHsJgRnQgfQdtJiECuWEMDAbQV61aCpsUrTh3"
        }
      ]
    }
```

### Version 2 of the DIDDoc

Time passes, and the [[ref: DID Controller]] of the `did:tdw` DID decides to
update its DID to a new version, version 2.

#### Target Version 2 DIDDoc

The [[ref: DID Controller]] constructs the new target DIDDoc (below) in
preparation for passing it into the process to [Update](#update-rotate) the `did:tdw`
DID.

```json
{
  "@context": [
    "https://www.w3.org/ns/did/v1",
    "https://w3id.org/security/multikey/v1",
    "https://identity.foundation/linked-vp/contexts/v1"
  ],
  "id": "did:tdw:migrated.example.com:4c99uuenu8gk6n3bgf09fuf350gx",
  "controller": [
    "did:tdw:migrated.example.com:4c99uuenu8gk6n3bgf09fuf350gx"
  ],
  "authentication": [
    "did:tdw:migrated.example.com:4c99uuenu8gk6n3bgf09fuf350gx#CpsUrTh3"
  ],
  "assertionMethod": [
    "did:tdw:migrated.example.com:4c99uuenu8gk6n3bgf09fuf350gx#gJqvqaYD"
  ],
  "verificationMethod": [
    {
      "id": "did:tdw:migrated.example.com:4c99uuenu8gk6n3bgf09fuf350gx#CpsUrTh3",
      "controller": "did:tdw:migrated.example.com:4c99uuenu8gk6n3bgf09fuf350gx",
      "type": "Multikey",
      "publicKeyMultibase": "z6MkuocstfAaHsJgRnQgfQdtJiECuWEMDAbQV61aCpsUrTh3"
    },
    {
      "id": "did:tdw:migrated.example.com:4c99uuenu8gk6n3bgf09fuf350gx#gJqvqaYD",
      "controller": "did:tdw:migrated.example.com:4c99uuenu8gk6n3bgf09fuf350gx",
      "type": "Multikey",
      "publicKeyMultibase": "z6MksNvDtgMutKMzjezRqj8JbYuCHNjHR5HBaF2ogJqvqaYD"
    }
  ],
  "service": [
    {
      "id": "did:tdw:example.com:4c99uuenu8gk6n3bgf09fuf350gx#whois",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": [
        "https://example.com/docs/4c99uuenu8gk6n3bgf09fuf350gx/whois.json"
      ]
    }
  ]
}
```

#### Version 2 Entry Hashing Input

To generate a new version of the DID, the [[ref: DID Controller]] needs to
provide the existing DID log file, and the new DIDDoc. The following processing is
done to create the new [[ref: DID log entry]]:

- The `entryHash` from the previous (first) log entry is made the first item in the new log entry.
- The `versionId` from the previous (first) log entry is retrieved, incremented and made the new `versionId` (second) item.
- The `versionTime` is generated as the current time, and made the new `versionTime` (third) item.
- The DIDDoc from the previous (first) log entry is extracted and then it and the new DIDDoc are passed into a [[ref: JSON Patch]] implementation to generate the `patch` that is the fourth item of the log entry.
- The resulting array is passed into the [`entryHash` generation process](#entry-hash-generation-and-validation) which outputs the `entryHash` for this log entry. The first item in the log entry is replaced with this new `entryHash`.
- The data integrity proof is generated added to the log entry as the sixth item, and the entire entry is added to the existing DID log.

The DID log file can now be published, optionally with an updated version of the corresponding `did:web` DID.

The following is the JSON pretty-print log entry for the second version of an example `did:tdw`. Things to note in this example:

- The data integrity proof `verificationMethod` is the `did:key` from the first log entry, and the `challenge` is the `entryHash` from this log entry.
- A new `updateKeys` item in the `parameters` has been added, rotating the key to control future updates to the DID.
- The [[ref: JSON Patch]] content that evolves the DIDDoc from version 1 to version 2.

```json
[
  "n12cnb197b6r3f3zzwwph5g22z3gzx4nx9qghnzvpf122aj9ara0",
  2,
  "2024-06-13T12:06:29Z",
  {
    "updateKeys": [
      "did:key:z6MksNvDtgMutKMzjezRqj8JbYuCHNjHR5HBaF2ogJqvqaYD"
    ]
  },
  {
    "patch": [
      {
        "op": "replace",
        "path": "/verificationMethod/1/publicKeyMultibase",
        "value": "z6Mkq7Qoa2LCvLCUiq9W2J9vXH1ooDqSX2ehWGUzCZSeAWLE"
      },
      {
        "op": "replace",
        "path": "/verificationMethod/1/controller",
        "value": "did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t"
      },
      {
        "op": "replace",
        "path": "/verificationMethod/1/id",
        "value": "did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CZSeAWLE"
      },
      {
        "op": "replace",
        "path": "/verificationMethod/0/publicKeyMultibase",
        "value": "z6MksNvDtgMutKMzjezRqj8JbYuCHNjHR5HBaF2ogJqvqaYD"
      },
      {
        "op": "replace",
        "path": "/verificationMethod/0/controller",
        "value": "did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t"
      },
      {
        "op": "replace",
        "path": "/verificationMethod/0/id",
        "value": "did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#gJqvqaYD"
      },
      {
        "op": "replace",
        "path": "/assertionMethod/0",
        "value": "did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CZSeAWLE"
      },
      {
        "op": "replace",
        "path": "/authentication/0",
        "value": "did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#gJqvqaYD"
      },
      {
        "op": "replace",
        "path": "/controller",
        "value": [
          "did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t"
        ]
      },
      {
        "op": "replace",
        "path": "/id",
        "value": "did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t"
      },
      {
        "op": "add",
        "path": "/@context/2",
        "value": "https://identity.foundation/linked-vp/contexts/v1"
      },
      {
        "op": "add",
        "path": "/service",
        "value": [
          {
            "id": "did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#whois",
            "type": "LinkedVerifiablePresentation",
            "serviceEndpoint": [
              "https://example.com/docs/c6ee1vru45p8cbt3a10ubw6pz67t/whois.json"
            ]
          }
        ]
      }
    ]
  },
  [
    {
      "type": "DataIntegrityProof",
      "cryptosuite": "eddsa-jcs-2022",
      "verificationMethod": "did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B",
      "created": "2024-06-13T12:06:29Z",
      "proofPurpose": "authentication",
      "challenge": "n12cnb197b6r3f3zzwwph5g22z3gzx4nx9qghnzvpf122aj9ara0",
      "proofValue": "z3PE2UGWx4MXYCWWh1SCAZU2ituDSVh6rob1PAj31oLsxtMx9ox2K5petgvCzEkiCuBz3iP5GXyXQFNvaFZpa9Y13"
    }
  ]
]
```

#### Log File For Version 2

The new version 2 `did.jsonl` file contains two entries, one for each version
of the DIDDoc.

```json
["c6ee1vru45p8cbt3a10ubw6pz67t",1,"2024-06-13T12:06:29Z",{"method":"did:tdw:1","scid":"c6ee1vru45p8cbt3a10ubw6pz67t","updateKeys":["did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"]},{"value":{"@context":["https://www.w3.org/ns/did/v1","https://w3id.org/security/multikey/v1"],"id":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t","controller":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t","authentication":["did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#5b48Zj6B"],"assertionMethod":["did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CpsUrTh3"],"verificationMethod":[{"id":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#5b48Zj6B","controller":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t","type":"Multikey","publicKeyMultibase":"z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"},{"id":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CpsUrTh3","controller":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t","type":"Multikey","publicKeyMultibase":"z6MkuocstfAaHsJgRnQgfQdtJiECuWEMDAbQV61aCpsUrTh3"}]}},[{"type":"DataIntegrityProof","cryptosuite":"eddsa-jcs-2022","verificationMethod":"did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B","created":"2024-06-13T12:06:29Z","proofPurpose":"authentication","challenge":"3dunqt4uet42kw71e1knnd3q69mfc9j4dq6dvzqzm9mrdpg6fyh0","proofValue":"z3UQwVFPxeXzb82DTaXQf9AwEst7NB22doLbZVou2CNs1fnGbX1mDNVMdrGM9868vauLSmPeGex7BzRcKaEm5xvRA"}]]
["n12cnb197b6r3f3zzwwph5g22z3gzx4nx9qghnzvpf122aj9ara0",2,"2024-06-13T12:06:29Z",{"updateKeys":["did:key:z6MksNvDtgMutKMzjezRqj8JbYuCHNjHR5HBaF2ogJqvqaYD"]},{"patch":[{"op":"replace","path":"/verificationMethod/1/publicKeyMultibase","value":"z6Mkq7Qoa2LCvLCUiq9W2J9vXH1ooDqSX2ehWGUzCZSeAWLE"},{"op":"replace","path":"/verificationMethod/1/controller","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t"},{"op":"replace","path":"/verificationMethod/1/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CZSeAWLE"},{"op":"replace","path":"/verificationMethod/0/publicKeyMultibase","value":"z6MksNvDtgMutKMzjezRqj8JbYuCHNjHR5HBaF2ogJqvqaYD"},{"op":"replace","path":"/verificationMethod/0/controller","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t"},{"op":"replace","path":"/verificationMethod/0/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#gJqvqaYD"},{"op":"replace","path":"/assertionMethod/0","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CZSeAWLE"},{"op":"replace","path":"/authentication/0","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#gJqvqaYD"},{"op":"replace","path":"/controller","value":["did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t"]},{"op":"replace","path":"/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t"},{"op":"add","path":"/@context/2","value":"https://identity.foundation/linked-vp/contexts/v1"},{"op":"add","path":"/service","value":[{"id":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#whois","type":"LinkedVerifiablePresentation","serviceEndpoint":["https://example.com/docs/c6ee1vru45p8cbt3a10ubw6pz67t/whois.json"]}]}]},[{"type":"DataIntegrityProof","cryptosuite":"eddsa-jcs-2022","verificationMethod":"did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B","created":"2024-06-13T12:06:29Z","proofPurpose":"authentication","challenge":"n12cnb197b6r3f3zzwwph5g22z3gzx4nx9qghnzvpf122aj9ara0","proofValue":"z3PE2UGWx4MXYCWWh1SCAZU2ituDSVh6rob1PAj31oLsxtMx9ox2K5petgvCzEkiCuBz3iP5GXyXQFNvaFZpa9Y13"}]]
```

#### Log File For Version 3-7

The same process is repeated for versions 3-7 of the DID. The `did.jsonl` file
(below) contains six entries, one for each version of the DIDDoc. Note in the
sixth version of the DID, the inclusion in the parameters of the activation of
the use of pre-rotation, and the `nextKeyHashes` -- pre-rotation keys. In the
seventh (and last) version of the DID, the DID is deactivated.

```json
["c6ee1vru45p8cbt3a10ubw6pz67t",1,"2024-06-13T12:06:29Z",{"method":"did:tdw:1","scid":"c6ee1vru45p8cbt3a10ubw6pz67t","updateKeys":["did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"]},{"value":{"@context":["https://www.w3.org/ns/did/v1","https://w3id.org/security/multikey/v1"],"id":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t","controller":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t","authentication":["did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#5b48Zj6B"],"assertionMethod":["did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CpsUrTh3"],"verificationMethod":[{"id":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#5b48Zj6B","controller":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t","type":"Multikey","publicKeyMultibase":"z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"},{"id":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CpsUrTh3","controller":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t","type":"Multikey","publicKeyMultibase":"z6MkuocstfAaHsJgRnQgfQdtJiECuWEMDAbQV61aCpsUrTh3"}]}},[{"type":"DataIntegrityProof","cryptosuite":"eddsa-jcs-2022","verificationMethod":"did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B","created":"2024-06-13T12:06:29Z","proofPurpose":"authentication","challenge":"3dunqt4uet42kw71e1knnd3q69mfc9j4dq6dvzqzm9mrdpg6fyh0","proofValue":"z3UQwVFPxeXzb82DTaXQf9AwEst7NB22doLbZVou2CNs1fnGbX1mDNVMdrGM9868vauLSmPeGex7BzRcKaEm5xvRA"}]]
["n12cnb197b6r3f3zzwwph5g22z3gzx4nx9qghnzvpf122aj9ara0",2,"2024-06-13T12:06:29Z",{"updateKeys":["did:key:z6MksNvDtgMutKMzjezRqj8JbYuCHNjHR5HBaF2ogJqvqaYD"]},{"patch":[{"op":"replace","path":"/verificationMethod/1/publicKeyMultibase","value":"z6Mkq7Qoa2LCvLCUiq9W2J9vXH1ooDqSX2ehWGUzCZSeAWLE"},{"op":"replace","path":"/verificationMethod/1/controller","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t"},{"op":"replace","path":"/verificationMethod/1/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CZSeAWLE"},{"op":"replace","path":"/verificationMethod/0/publicKeyMultibase","value":"z6MksNvDtgMutKMzjezRqj8JbYuCHNjHR5HBaF2ogJqvqaYD"},{"op":"replace","path":"/verificationMethod/0/controller","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t"},{"op":"replace","path":"/verificationMethod/0/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#gJqvqaYD"},{"op":"replace","path":"/assertionMethod/0","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CZSeAWLE"},{"op":"replace","path":"/authentication/0","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#gJqvqaYD"},{"op":"replace","path":"/controller","value":["did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t"]},{"op":"replace","path":"/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t"},{"op":"add","path":"/@context/2","value":"https://identity.foundation/linked-vp/contexts/v1"},{"op":"add","path":"/service","value":[{"id":"did:tdw:example.com:c6ee1vru45p8cbt3a10ubw6pz67t#whois","type":"LinkedVerifiablePresentation","serviceEndpoint":["https://example.com/docs/c6ee1vru45p8cbt3a10ubw6pz67t/whois.json"]}]}]},[{"type":"DataIntegrityProof","cryptosuite":"eddsa-jcs-2022","verificationMethod":"did:key:z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B","created":"2024-06-13T12:06:29Z","proofPurpose":"authentication","challenge":"n12cnb197b6r3f3zzwwph5g22z3gzx4nx9qghnzvpf122aj9ara0","proofValue":"z3PE2UGWx4MXYCWWh1SCAZU2ituDSVh6rob1PAj31oLsxtMx9ox2K5petgvCzEkiCuBz3iP5GXyXQFNvaFZpa9Y13"}]]
["f65mh8vmhxevkxv5era62v5ahp79tzytnxk5bdmjwzkv4z5v83u0",3,"2024-06-13T12:06:29Z",{"updateKeys":["did:key:z6Mkr2D4ixckmQx8tAVvXEhMuaMhzahxe61qJt7G9vYyiXiJ"]},{"patch":[{"op":"add","path":"/service/1","value":{"id":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#didcomm","type":"DIDCommMessaging","serviceEndpoint":{"uri":"https://example.com/didcomm","accept":["didcomm/v2","didcomm/aip2;env=rfc587"],"routingKeys":["did:example:somemediator#somekey"]}}},{"op":"replace","path":"/verificationMethod/1/publicKeyMultibase","value":"z6MkjnDzaWSBfQFmzyPvhcaABbEBQiuCBRdyQNq5kkHS31Z4"},{"op":"replace","path":"/verificationMethod/1/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#kkHS31Z4"},{"op":"replace","path":"/verificationMethod/0/publicKeyMultibase","value":"z6Mkr2D4ixckmQx8tAVvXEhMuaMhzahxe61qJt7G9vYyiXiJ"},{"op":"replace","path":"/verificationMethod/0/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#9vYyiXiJ"},{"op":"add","path":"/verificationMethod/2","value":{"id":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#qnYZ6fWH","controller":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t","type":"Multikey","publicKeyMultibase":"z6LSdYjdAE7ZY1Gh5VPAxDJdgbg45Lq6im3N9o6HqnYZ6fWH"}},{"op":"replace","path":"/assertionMethod/0","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#kkHS31Z4"},{"op":"replace","path":"/authentication/0","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#9vYyiXiJ"},{"op":"add","path":"/@context/3","value":"https://didcomm.org/messaging/v2"},{"op":"add","path":"/keyAgreement","value":["did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#qnYZ6fWH"]}]},[{"type":"DataIntegrityProof","cryptosuite":"eddsa-jcs-2022","verificationMethod":"did:key:z6MksNvDtgMutKMzjezRqj8JbYuCHNjHR5HBaF2ogJqvqaYD","created":"2024-06-13T12:06:29Z","proofPurpose":"authentication","challenge":"f65mh8vmhxevkxv5era62v5ahp79tzytnxk5bdmjwzkv4z5v83u0","proofValue":"z2F9Wo7Bf2MztZskLV2k94HDwt159VgjYUVoJELyYm1Bo2gutgTq8jxjXx7ASk5jPEd6ZgxNrCbrfYUPvy4q4nftf"}]]
["nh0y075w5gm3n6qv5n63wcxgt4v90wte5a4p8utfbvc1xeucu73g",4,"2024-06-13T12:06:29Z",{"updateKeys":["did:key:z6MkkmrDWT9n8rmAVfEvuyBFroc6RFNffAoycrLw4jDJpwPh"]},{"patch":[{"op":"replace","path":"/keyAgreement/0","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CAHUs8cU"},{"op":"replace","path":"/verificationMethod/2/publicKeyMultibase","value":"z6LSh1TgaytstJw2EnB8gRTZjJaHRVrUQ9K3SAofCAHUs8cU"},{"op":"replace","path":"/verificationMethod/2/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#CAHUs8cU"},{"op":"replace","path":"/verificationMethod/1/publicKeyMultibase","value":"z6MkhoA3GQu8Sek1GFrMpmZNFxy2fSXVzzMggdndDuAWQAnf"},{"op":"replace","path":"/verificationMethod/1/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#DuAWQAnf"},{"op":"replace","path":"/verificationMethod/0/publicKeyMultibase","value":"z6MkkmrDWT9n8rmAVfEvuyBFroc6RFNffAoycrLw4jDJpwPh"},{"op":"replace","path":"/verificationMethod/0/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#4jDJpwPh"},{"op":"replace","path":"/assertionMethod/0","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#DuAWQAnf"},{"op":"replace","path":"/authentication/0","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#4jDJpwPh"},{"op":"add","path":"/alsoKnownAs","value":["did:web:example.com"]}]},[{"type":"DataIntegrityProof","cryptosuite":"eddsa-jcs-2022","verificationMethod":"did:key:z6Mkr2D4ixckmQx8tAVvXEhMuaMhzahxe61qJt7G9vYyiXiJ","created":"2024-06-13T12:06:29Z","proofPurpose":"authentication","challenge":"nh0y075w5gm3n6qv5n63wcxgt4v90wte5a4p8utfbvc1xeucu73g","proofValue":"z3hD5stvY1UnpXGk7dCunkG2VgZzBXdpckCNPn55m6gYXKuDMtPnppgGmeTCGUg1DWhLZDUTDnp44Wxst4hrvzdjU"}]]
["4d37xup50ztumvxvpq60fm8nwumwdytppw03f4m1vg75kmyy3heg",5,"2024-06-13T12:06:29Z",{"updateKeys":["did:key:z6MkhGC8KFeSQq8y7Jt2wUgyyTgwJAbMt16gKEwCBgxQ25XL","did:key:z6MktpbfYB3usrBJYN5uEou8o3iFfurWTCWUHEMHUn97YusZ"]},{"patch":[{"op":"remove","path":"/keyAgreement"},{"op":"remove","path":"/verificationMethod/2"},{"op":"replace","path":"/verificationMethod/1/publicKeyMultibase","value":"z6MktpbfYB3usrBJYN5uEou8o3iFfurWTCWUHEMHUn97YusZ"},{"op":"replace","path":"/verificationMethod/1/controller","value":"did:key:z6MktpbfYB3usrBJYN5uEou8o3iFfurWTCWUHEMHUn97YusZ"},{"op":"replace","path":"/verificationMethod/1/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#Un97YusZ"},{"op":"replace","path":"/verificationMethod/0/publicKeyMultibase","value":"z6MkhGC8KFeSQq8y7Jt2wUgyyTgwJAbMt16gKEwCBgxQ25XL"},{"op":"replace","path":"/verificationMethod/0/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#BgxQ25XL"},{"op":"remove","path":"/assertionMethod"},{"op":"replace","path":"/authentication/0","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#BgxQ25XL"},{"op":"add","path":"/authentication/1","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#Un97YusZ"},{"op":"add","path":"/controller/1","value":"did:key:z6MktpbfYB3usrBJYN5uEou8o3iFfurWTCWUHEMHUn97YusZ"}]},[{"type":"DataIntegrityProof","cryptosuite":"eddsa-jcs-2022","verificationMethod":"did:key:z6MkkmrDWT9n8rmAVfEvuyBFroc6RFNffAoycrLw4jDJpwPh","created":"2024-06-13T12:06:29Z","proofPurpose":"authentication","challenge":"4d37xup50ztumvxvpq60fm8nwumwdytppw03f4m1vg75kmyy3heg","proofValue":"z2BPTnCwC29FVJ7QQLNHeEsUo5mG4J53ZiaDE7SNsitUnsTNim8VsCGsEEEJrza2UoaZy3C7kxjvYwboqNDCiLoS1"}]]
["ztxfqwh57f8bytju3v42jqqzakj723b8p1bmuj1b4gmjfe9jdfh0",6,"2024-06-13T12:06:29Z",{"updateKeys":["did:key:z6MkvVjSMp6xsghjQP54WndyEAjKHduUVxxqm1oMfdPocsYi"],"prerotate":true,"nextKeyHashes":["yb6xe3kub8xdwgq4y98jafz5bnb0xydd2b17ymd4607v7k8b4y9g"]},{"patch":[{"op":"remove","path":"/verificationMethod/1"},{"op":"replace","path":"/verificationMethod/0/publicKeyMultibase","value":"z6MkvVjSMp6xsghjQP54WndyEAjKHduUVxxqm1oMfdPocsYi"},{"op":"replace","path":"/verificationMethod/0/id","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#fdPocsYi"},{"op":"remove","path":"/authentication/1"},{"op":"replace","path":"/authentication/0","value":"did:tdw:migrated.example.com:c6ee1vru45p8cbt3a10ubw6pz67t#fdPocsYi"},{"op":"remove","path":"/controller/1"}]},[{"type":"DataIntegrityProof","cryptosuite":"eddsa-jcs-2022","verificationMethod":"did:key:z6MkhGC8KFeSQq8y7Jt2wUgyyTgwJAbMt16gKEwCBgxQ25XL","created":"2024-06-13T12:06:29Z","proofPurpose":"authentication","challenge":"ztxfqwh57f8bytju3v42jqqzakj723b8p1bmuj1b4gmjfe9jdfh0","proofValue":"z3zweU6AeDKSLE3YncGg9geFXejTgTrKQSeqxLzLWHczrWNR7QgLvd2ByQJ7bMjqnyKU4CRTY5Xs9FFgFQ8m5sfyx"}]]
["3htb6726wbt6f4v8ryphdxaq4rgw3ryj3fp3qe1r1djehrwxk2mg",7,"2024-06-13T12:06:29Z",{"deactivated":true},{"patch":[{"op":"remove","path":"/verificationMethod/0"},{"op":"remove","path":"/authentication/0"},{"op":"add","path":"/assertionMethod","value":[]},{"op":"add","path":"/capabilityInvocation","value":[]},{"op":"add","path":"/capabilityDelegation","value":[]},{"op":"add","path":"/keyAgreement","value":[]}]},[{"type":"DataIntegrityProof","cryptosuite":"eddsa-jcs-2022","verificationMethod":"did:key:z6MkvVjSMp6xsghjQP54WndyEAjKHduUVxxqm1oMfdPocsYi","created":"2024-06-13T12:06:29Z","proofPurpose":"authentication","challenge":"3htb6726wbt6f4v8ryphdxaq4rgw3ryj3fp3qe1r1djehrwxk2mg","proofValue":"ztXPCXPGemS2m13i7a5tZJ48U69xYhNA17rdtRR2LMzwBz6QCiZAomaQTmY6LFUvgDrifiQVkTj9FXqcYkcN4eXW"}]]
```

And so on...
