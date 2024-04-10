## `did:tdw` Example

The following shows the evolution of a `did:tdw` from inception through several
versions, showing the DID, DIDDoc, [[ref: DID Log]], and some of the
intermediate data structures.

In the following, all of the data for the [[ref: DID log entries]] are displayed
as prettified JSON for readability. In the log itself, the JSON has all
whitespace removed, and each line ends with a `CR`.

### DID Creation Data

These examples show the important structures used in the [Create (Register)](#create-register) operation for a `did:tdw` DID.

#### DIDDoc with SCID Placeholders

This is the version of the DIDDoc that the [[ref: DID Controller]] constructs
(however they see fit) and passes into the [SCID Generation Process](#scid-generation-and-validation).

```json
{
      "@context": [
        "https://www.w3.org/ns/did/v1",
        "https://w3id.org/security/multikey/v1"
      ],
      "id": "did:web:example.com:{SCID}",
      "controller": "did:web:example.com:{SCID}",
      "authentication": [
        "did:web:example.com:{SCID}#FFhXVfsx"
      ],
      "assertionMethod": [
        "did:web:example.com:{SCID}#CPixwJ8x"
      ],
      "verificationMethod": [
        {
          "id": "did:web:example.com:{SCID}#FFhXVfsx",
          "controller": "did:web:example.com:{SCID}",
          "type": "Multikey",
          "publicKeyMultibase": "z6MkkXKMSiE7mXvGcR2KUpeJXwT7MPXZSBC6HZw9FFhXVfsx"
        },
        {
          "id": "did:web:example.com:{SCID}#CPixwJ8x",
          "controller": "did:web:example.com:{SCID}",
          "type": "Multikey",
          "publicKeyMultibase": "z6Mkg8FdKNRt4NLXm5YSUZVGWzK8vvS3DJByxAqHCPixwJ8x"
        }
      ]
    }
```

#### DIDDoc with SCID In Place

After the SCID is generated, the `{SCID}` placeholders are replaced by the generated [[ref: SCID]] value.

```json
{
  "@context": [
    "https://www.w3.org/ns/did/v1",
    "https://w3id.org/security/multikey/v1"
  ],
  "id": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te",
  "controller": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te",
  "authentication": [
    "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx"
  ],
  "assertionMethod": [
    "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x"
  ],
  "verificationMethod": [
    {
      "id": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx",
      "controller": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te",
      "type": "Multikey",
      "publicKeyMultibase": "z6MkkXKMSiE7mXvGcR2KUpeJXwT7MPXZSBC6HZw9FFhXVfsx"
    },
    {
      "id": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x",
      "controller": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te",
      "type": "Multikey",
      "publicKeyMultibase": "z6Mkg8FdKNRt4NLXm5YSUZVGWzK8vvS3DJByxAqHCPixwJ8x"
    }
  ]
}
```

#### Entry Hash Generation Input

The first item in the entry hashing input for Version 1 of the DIDDoc is SCID of
the DID. The fifth item, containing the first version DIDDoc content is the full
DIDDoc (as indicated by the `value` item).

```json
[
  "ke465curdwjzrrp5x5ut92te",
  1,
  "2024-04-03T03:47:51Z",
  {
    "method": "did:tdw:1",
    "scid": "ke465curdwjzrrp5x5ut92te"
  },
  {
    "value": {
      "@context": [
        "https://www.w3.org/ns/did/v1",
        "https://w3id.org/security/multikey/v1"
      ],
      "id": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te",
      "controller": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te",
      "authentication": [
        "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx"
      ],
      "assertionMethod": [
        "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x"
      ],
      "verificationMethod": [
        {
          "id": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx",
          "controller": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te",
          "type": "Multikey",
          "publicKeyMultibase": "z6MkkXKMSiE7mXvGcR2KUpeJXwT7MPXZSBC6HZw9FFhXVfsx"
        },
        {
          "id": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x",
          "controller": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te",
          "type": "Multikey",
          "publicKeyMultibase": "z6Mkg8FdKNRt4NLXm5YSUZVGWzK8vvS3DJByxAqHCPixwJ8x"
        }
      ]
    }
  }
]
```

#### First Log Entry

The following is the JSON prettified version of the entry log file that is published
as the `did.jsonl` file. When published, all extraneous whitespace is removed, as
shown in the block below the pretty-printed version.

```json
[
  "xkuu1nwynw5ymfv4f1np2xbmg21k4vn1rrvg3ngpdmx482c2ce20",
  1,
  "2024-04-03T03:47:51Z",
  {
    "method": "did:tdw:1",
    "scid": "ke465curdwjzrrp5x5ut92te"
  },
  {
    "value": {
      "@context": [
        "https://www.w3.org/ns/did/v1",
        "https://w3id.org/security/multikey/v1"
      ],
      "id": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te",
      "controller": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te",
      "authentication": [
        "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx"
      ],
      "assertionMethod": [
        "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x"
      ],
      "verificationMethod": [
        {
          "id": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx",
          "controller": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te",
          "type": "Multikey",
          "publicKeyMultibase": "z6MkkXKMSiE7mXvGcR2KUpeJXwT7MPXZSBC6HZw9FFhXVfsx"
        },
        {
          "id": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x",
          "controller": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te",
          "type": "Multikey",
          "publicKeyMultibase": "z6Mkg8FdKNRt4NLXm5YSUZVGWzK8vvS3DJByxAqHCPixwJ8x"
        }
      ]
    }
  },
  {
    "type": "DataIntegrityProof",
    "created": "2024-04-03T03:47:51Z",
    "verificationMethod": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx",
    "cryptosuite": "eddsa-2022",
    "proofPurpose": "authentication",
    "challenge": "xkuu1nwynw5ymfv4f1np2xbmg21k4vn1rrvg3ngpdmx482c2ce20",
    "proofValue": "zK7pASjX3ou7t2bDuU43sWzG4E8B3TTDFgmY8AiFLahPaLzXn4fGrXksKbWr6o2RLr7rCTT2VRAgc8F9LQKLEJkg"
  }
]
```

The same content as it is found in the `did.jsonl` file:

```json
["xkuu1nwynw5ymfv4f1np2xbmg21k4vn1rrvg3ngpdmx482c2ce20",1,"2024-04-03T03:47:51Z",{"method":"did:tdw:1","scid":"ke465curdwjzrrp5x5ut92te"},{"value":{"@context":["https://www.w3.org/ns/did/v1","https://w3id.org/security/multikey/v1"],"id":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te","controller":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te","authentication":["did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx"],"assertionMethod":["did:tdw:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x"],"verificationMethod":[{"id":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx","controller":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te","type":"Multikey","publicKeyMultibase":"z6MkkXKMSiE7mXvGcR2KUpeJXwT7MPXZSBC6HZw9FFhXVfsx"},{"id":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x","controller":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te","type":"Multikey","publicKeyMultibase":"z6Mkg8FdKNRt4NLXm5YSUZVGWzK8vvS3DJByxAqHCPixwJ8x"}]}},{"type":"DataIntegrityProof","created":"2024-04-03T03:47:51Z","verificationMethod":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx","cryptosuite":"eddsa-2022","proofPurpose":"authentication","challenge":"xkuu1nwynw5ymfv4f1np2xbmg21k4vn1rrvg3ngpdmx482c2ce20","proofValue":"zK7pASjX3ou7t2bDuU43sWzG4E8B3TTDFgmY8AiFLahPaLzXn4fGrXksKbWr6o2RLr7rCTT2VRAgc8F9LQKLEJkg"}]
```

#### `did:web` Version of DIDDoc

As noted in the [publishing a parallel `did:web`
DID](#publishing-a-parallel-didweb-did) section of this specification, here is
what the `did:web` DIDDoc looks like for the `did:tdw` above.

```json
{
  "@context": [
    "https://www.w3.org/ns/did/v1",
    "https://w3id.org/security/multikey/v1"
  ],
  "id": "did:web:example.com:ke465curdwjzrrp5x5ut92te",
  "alsoKnownAs": ["did:tdw:example.com:ke465curdwjzrrp5x5ut92te"],
  "controller": "did:web:example.com:ke465curdwjzrrp5x5ut92te",
  "authentication": [
    "did:web:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx"
  ],
  "assertionMethod": [
    "did:web:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x"
  ],
  "verificationMethod": [
    {
      "id": "did:web:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx",
      "controller": "did:web:example.com:ke465curdwjzrrp5x5ut92te",
      "type": "Multikey",
      "publicKeyMultibase": "z6MkkXKMSiE7mXvGcR2KUpeJXwT7MPXZSBC6HZw9FFhXVfsx"
    },
    {
      "id": "did:web:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x",
      "controller": "did:web:example.com:ke465curdwjzrrp5x5ut92te",
      "type": "Multikey",
      "publicKeyMultibase": "z6Mkg8FdKNRt4NLXm5YSUZVGWzK8vvS3DJByxAqHCPixwJ8x"
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
  "id": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te",
  "controller": [
    "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"
  ],
  "authentication": [
    "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#5b48Zj6B"
  ],
  "assertionMethod": [
    "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#CpsUrTh3"
  ],
  "verificationMethod": [
    {
      "id": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#5b48Zj6B",
      "controller": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te",
      "type": "Multikey",
      "publicKeyMultibase": "z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"
    },
    {
      "id": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#CpsUrTh3",
      "controller": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te",
      "type": "Multikey",
      "publicKeyMultibase": "z6MkuocstfAaHsJgRnQgfQdtJiECuWEMDAbQV61aCpsUrTh3"
    }
  ],
  "service": [
    {
      "id": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#whois",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": [
        "https://example.com/docs/ke465curdwjzrrp5x5ut92te/whois.json"
      ]
    }
  ]
}
```

#### Version 2 Entry Hashing Input

The first item in the entry hashing input for Version 2 of the DIDDoc is the
entry hash generated for the Version 1 of the DIDDoc. The fifth item, containing the new
version DIDDoc content is in the form of a [[spec:rfc6902]] JSON Patch (as
indicated by the `patch` item), and are the set of operations to transition the
DIDDoc from version 1 to this new version 2 DIDDoc.

```json
[
  "xkuu1nwynw5ymfv4f1np2xbmg21k4vn1rrvg3ngpdmx482c2ce20",
  2,
  "2024-04-03T03:47:51Z",
  {},
  {
    "patch": [
      {
        "op": "replace",
        "path": "/verificationMethod/1/publicKeyMultibase",
        "value": "z6MkuocstfAaHsJgRnQgfQdtJiECuWEMDAbQV61aCpsUrTh3"
      },
      {
        "op": "replace",
        "path": "/verificationMethod/1/controller",
        "value": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"
      },
      {
        "op": "replace",
        "path": "/verificationMethod/1/id",
        "value": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#CpsUrTh3"
      },
      {
        "op": "replace",
        "path": "/verificationMethod/0/publicKeyMultibase",
        "value": "z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"
      },
      {
        "op": "replace",
        "path": "/verificationMethod/0/controller",
        "value": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"
      },
      {
        "op": "replace",
        "path": "/verificationMethod/0/id",
        "value": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#5b48Zj6B"
      },
      {
        "op": "replace",
        "path": "/assertionMethod/0",
        "value": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#CpsUrTh3"
      },
      {
        "op": "replace",
        "path": "/authentication/0",
        "value": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#5b48Zj6B"
      },
      {
        "op": "replace",
        "path": "/controller",
        "value": [
          "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"
        ]
      },
      {
        "op": "replace",
        "path": "/id",
        "value": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"
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
            "id": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#whois",
            "type": "LinkedVerifiablePresentation",
            "serviceEndpoint": [
              "https://example.com/docs/ke465curdwjzrrp5x5ut92te/whois.json"
            ]
          }
        ]
      }
    ]
  }
]
```

#### Log File For Version 2

The new version 2 `did.jsonl` file contains two entries, one for each version
of the DIDDoc. The data integrity proof on the version 2 entry **MUST** be from
an `authentication` key from the version 1 DIDDoc.

```json
["xkuu1nwynw5ymfv4f1np2xbmg21k4vn1rrvg3ngpdmx482c2ce20",1,"2024-04-03T03:47:51Z",{"method":"did:tdw:1","scid":"ke465curdwjzrrp5x5ut92te"},{"value":{"@context":["https://www.w3.org/ns/did/v1","https://w3id.org/security/multikey/v1"],"id":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te","controller":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te","authentication":["did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx"],"assertionMethod":["did:tdw:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x"],"verificationMethod":[{"id":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx","controller":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te","type":"Multikey","publicKeyMultibase":"z6MkkXKMSiE7mXvGcR2KUpeJXwT7MPXZSBC6HZw9FFhXVfsx"},{"id":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x","controller":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te","type":"Multikey","publicKeyMultibase":"z6Mkg8FdKNRt4NLXm5YSUZVGWzK8vvS3DJByxAqHCPixwJ8x"}]}},{"type":"DataIntegrityProof","created":"2024-04-03T03:47:51Z","verificationMethod":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx","cryptosuite":"eddsa-2022","proofPurpose":"authentication","challenge":"xkuu1nwynw5ymfv4f1np2xbmg21k4vn1rrvg3ngpdmx482c2ce20","proofValue":"zK7pASjX3ou7t2bDuU43sWzG4E8B3TTDFgmY8AiFLahPaLzXn4fGrXksKbWr6o2RLr7rCTT2VRAgc8F9LQKLEJkg"}]
["zbuqyfaytakn9bhqhwrn0f3kh3fc5trz5qxmj91ay6rn71qhcnw0",2,"2024-04-03T03:47:51Z",{},{"patch":[{"op":"replace","path":"/verificationMethod/1/publicKeyMultibase","value":"z6MkuocstfAaHsJgRnQgfQdtJiECuWEMDAbQV61aCpsUrTh3"},{"op":"replace","path":"/verificationMethod/1/controller","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"},{"op":"replace","path":"/verificationMethod/1/id","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#CpsUrTh3"},{"op":"replace","path":"/verificationMethod/0/publicKeyMultibase","value":"z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"},{"op":"replace","path":"/verificationMethod/0/controller","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"},{"op":"replace","path":"/verificationMethod/0/id","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#5b48Zj6B"},{"op":"replace","path":"/assertionMethod/0","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#CpsUrTh3"},{"op":"replace","path":"/authentication/0","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#5b48Zj6B"},{"op":"replace","path":"/controller","value":["did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"]},{"op":"replace","path":"/id","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"},{"op":"add","path":"/@context/2","value":"https://identity.foundation/linked-vp/contexts/v1"},{"op":"add","path":"/service","value":[{"id":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#whois","type":"LinkedVerifiablePresentation","serviceEndpoint":["https://example.com/docs/ke465curdwjzrrp5x5ut92te/whois.json"]}]}]},{"type":"DataIntegrityProof","created":"2024-04-03T03:47:51Z","verificationMethod":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx","cryptosuite":"eddsa-2022","proofPurpose":"authentication","challenge":"zbuqyfaytakn9bhqhwrn0f3kh3fc5trz5qxmj91ay6rn71qhcnw0","proofValue":"z4zn3AVWC76rDoDtvNW2ospTPC3vDMfbxcZ383AkDun43KUBhBAv3ZJcE9zRXT8K3pHEDBaYvc19Q1weH5zoMa2Lf"}]
```

### Version 3

#### Version 3 Target DIDDoc

Here is the target update for the version 3 DIDDoc, as constructed by the DID Controller. It is the data used as input to the `did:tdw` log entry generation process.

```json
{
  "@context": [
    "https://www.w3.org/ns/did/v1",
    "https://w3id.org/security/multikey/v1",
    "https://identity.foundation/linked-vp/contexts/v1",
    "https://didcomm.org/messaging/v2"
  ],
  "id": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te",
  "controller": [
    "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"
  ],
  "authentication": [
    "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#gJqvqaYD"
  ],
  "assertionMethod": [
    "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#CZSeAWLE"
  ],
  "keyAgreement": [
    "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#qnYZ6fWH"
  ],
  "verificationMethod": [
    {
      "id": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#gJqvqaYD",
      "controller": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te",
      "type": "Multikey",
      "publicKeyMultibase": "z6MksNvDtgMutKMzjezRqj8JbYuCHNjHR5HBaF2ogJqvqaYD"
    },
    {
      "id": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#CZSeAWLE",
      "controller": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te",
      "type": "Multikey",
      "publicKeyMultibase": "z6Mkq7Qoa2LCvLCUiq9W2J9vXH1ooDqSX2ehWGUzCZSeAWLE"
    },
    {
      "id": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#qnYZ6fWH",
      "controller": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te",
      "type": "Multikey",
      "publicKeyMultibase": "z6LSdYjdAE7ZY1Gh5VPAxDJdgbg45Lq6im3N9o6HqnYZ6fWH"
    }
  ],
  "service": [
    {
      "id": "did:tdw:example.com:ke465curdwjzrrp5x5ut92te#whois",
      "type": "LinkedVerifiablePresentation",
      "serviceEndpoint": [
        "https://example.com/docs/ke465curdwjzrrp5x5ut92te/whois.json"
      ]
    },
    {
      "id": "did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#didcomm",
      "type": "DIDCommMessaging",
      "serviceEndpoint": {
        "uri": "https://example.com/didcomm",
        "accept": [
          "didcomm/v2",
          "didcomm/aip2;env=rfc587"
        ],
        "routingKeys": [
          "did:example:somemediator#somekey"
        ]
      }
    }
  ]
}
```

#### Log File For Version 3

The new version 3 `did.jsonl` file contains three entries, one for each version
of the DIDDoc. The data integrity proof on the version 3 entry **MUST** be from
an `authentication` key from the version 2 DIDDoc.

```json
["xkuu1nwynw5ymfv4f1np2xbmg21k4vn1rrvg3ngpdmx482c2ce20",1,"2024-04-03T03:47:51Z",{"method":"did:tdw:1","scid":"ke465curdwjzrrp5x5ut92te"},{"value":{"@context":["https://www.w3.org/ns/did/v1","https://w3id.org/security/multikey/v1"],"id":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te","controller":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te","authentication":["did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx"],"assertionMethod":["did:tdw:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x"],"verificationMethod":[{"id":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx","controller":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te","type":"Multikey","publicKeyMultibase":"z6MkkXKMSiE7mXvGcR2KUpeJXwT7MPXZSBC6HZw9FFhXVfsx"},{"id":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#CPixwJ8x","controller":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te","type":"Multikey","publicKeyMultibase":"z6Mkg8FdKNRt4NLXm5YSUZVGWzK8vvS3DJByxAqHCPixwJ8x"}]}},{"type":"DataIntegrityProof","created":"2024-04-03T03:47:51Z","verificationMethod":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx","cryptosuite":"eddsa-2022","proofPurpose":"authentication","challenge":"xkuu1nwynw5ymfv4f1np2xbmg21k4vn1rrvg3ngpdmx482c2ce20","proofValue":"zK7pASjX3ou7t2bDuU43sWzG4E8B3TTDFgmY8AiFLahPaLzXn4fGrXksKbWr6o2RLr7rCTT2VRAgc8F9LQKLEJkg"}]
["zbuqyfaytakn9bhqhwrn0f3kh3fc5trz5qxmj91ay6rn71qhcnw0",2,"2024-04-03T03:47:51Z",{},{"patch":[{"op":"replace","path":"/verificationMethod/1/publicKeyMultibase","value":"z6MkuocstfAaHsJgRnQgfQdtJiECuWEMDAbQV61aCpsUrTh3"},{"op":"replace","path":"/verificationMethod/1/controller","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"},{"op":"replace","path":"/verificationMethod/1/id","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#CpsUrTh3"},{"op":"replace","path":"/verificationMethod/0/publicKeyMultibase","value":"z6Mkw1KSvGWNAwSwWbcpwPgFARX4vKPa1xvcDMsJ5b48Zj6B"},{"op":"replace","path":"/verificationMethod/0/controller","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"},{"op":"replace","path":"/verificationMethod/0/id","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#5b48Zj6B"},{"op":"replace","path":"/assertionMethod/0","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#CpsUrTh3"},{"op":"replace","path":"/authentication/0","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#5b48Zj6B"},{"op":"replace","path":"/controller","value":["did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"]},{"op":"replace","path":"/id","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te"},{"op":"add","path":"/@context/2","value":"https://identity.foundation/linked-vp/contexts/v1"},{"op":"add","path":"/service","value":[{"id":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#whois","type":"LinkedVerifiablePresentation","serviceEndpoint":["https://example.com/docs/ke465curdwjzrrp5x5ut92te/whois.json"]}]}]},{"type":"DataIntegrityProof","created":"2024-04-03T03:47:51Z","verificationMethod":"did:tdw:example.com:ke465curdwjzrrp5x5ut92te#FFhXVfsx","cryptosuite":"eddsa-2022","proofPurpose":"authentication","challenge":"zbuqyfaytakn9bhqhwrn0f3kh3fc5trz5qxmj91ay6rn71qhcnw0","proofValue":"z4zn3AVWC76rDoDtvNW2ospTPC3vDMfbxcZ383AkDun43KUBhBAv3ZJcE9zRXT8K3pHEDBaYvc19Q1weH5zoMa2Lf"}]
["3856ukdk0tardcm40tg11qe8dche5w38b6z3cchrraabka80ejy0",3,"2024-04-03T03:47:51Z",{},{"patch":[{"op":"add","path":"/service/1","value":{"id":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#didcomm","type":"DIDCommMessaging","serviceEndpoint":{"uri":"https://example.com/didcomm","accept":["didcomm/v2","didcomm/aip2;env=rfc587"],"routingKeys":["did:example:somemediator#somekey"]}}},{"op":"replace","path":"/verificationMethod/1/publicKeyMultibase","value":"z6Mkq7Qoa2LCvLCUiq9W2J9vXH1ooDqSX2ehWGUzCZSeAWLE"},{"op":"replace","path":"/verificationMethod/1/id","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#CZSeAWLE"},{"op":"replace","path":"/verificationMethod/0/publicKeyMultibase","value":"z6MksNvDtgMutKMzjezRqj8JbYuCHNjHR5HBaF2ogJqvqaYD"},{"op":"replace","path":"/verificationMethod/0/id","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#gJqvqaYD"},{"op":"add","path":"/verificationMethod/2","value":{"id":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#qnYZ6fWH","controller":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te","type":"Multikey","publicKeyMultibase":"z6LSdYjdAE7ZY1Gh5VPAxDJdgbg45Lq6im3N9o6HqnYZ6fWH"}},{"op":"replace","path":"/assertionMethod/0","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#CZSeAWLE"},{"op":"replace","path":"/authentication/0","value":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#gJqvqaYD"},{"op":"add","path":"/@context/3","value":"https://didcomm.org/messaging/v2"},{"op":"add","path":"/keyAgreement","value":["did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#qnYZ6fWH"]}]},{"type":"DataIntegrityProof","created":"2024-04-03T03:47:51Z","verificationMethod":"did:tdw:migrated.example.com:ke465curdwjzrrp5x5ut92te#5b48Zj6B","cryptosuite":"eddsa-2022","proofPurpose":"authentication","challenge":"3856ukdk0tardcm40tg11qe8dche5w38b6z3cchrraabka80ejy0","proofValue":"z4e1hqAH9jNmwvfh1HvBDpB69Vq8nAGCdrCKa2ebK2kf7Pd2eNpPznKZRo9vfn72JjYabwe4drhQF9uQFmL4KxuiJ"}]
```

And so on...
