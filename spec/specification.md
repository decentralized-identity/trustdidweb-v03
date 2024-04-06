## did:tdw DID Method Specification

### Target System

The target system of the Trust DID Web (TDW) DID method is the host (or domain if the host is not specified) name when the domain specified by the DID is resolved through the Domain Name System (DNS).

### Method Name

The namestring that identifies this DID method is: `tdw`. A DID that uses
this method MUST begin with the following prefix: `did:tdw`. Per the DID
specification, this string MUST be in lowercase. The remainder of the DID, after
the prefix, is the [method-specific identifier](#method-specific-identifier),
specified below.

### Method-specific Identifier

The method specific identifier is a fully qualified domain name that is secured
by a TLS/SSL certificate with an optional path to the [[ref: DID Log]]. The
identifier **MUST** contain a [[ref: self-certifying identifier]] (SCID) as
either part of the subdomain component of the domain name, or as a component of
the optional path. The content of the [[ref: SCID]] is
[generated](#scid-generation-and-validation) in creating the DID. The formal
rules describing valid domain name syntax are described in [RFC1035], [RFC1123],
and [RFC2181].

The domain name component of the method specific identifier MUST match the
common name used in the SSL/TLS certificate, and it MUST NOT include IP
addresses. A port MAY be included and the colon MUST be percent encoded to
prevent a conflict with paths. Directories and subdirectories MAY optionally be
included, delimited by colons rather than slashes.

The [[ref: SCID]], a globally unique identifier, is generated as part of the
creation of the DID and placed into the DID identifier.

As specified in the Augmented Backus-Naur Form (ABNF) notation of
[RFC2234](https://datatracker.ietf.org/doc/html/rfc2234) below, the [[ref:
SCID]] **MUST** be present, but may be placed in the (optional) subdomain
component of the domain, or as a segment in the (optional) URL path. Examples
follow. The `domain-segment` and `path-segment` elements refer to the [ABNF
found in RFC3986 Generic URL
Syntax](https://datatracker.ietf.org/doc/html/rfc3986#page-49) as attempting to
replicate the full ABNF of those elements here would inevitably be done
incorrectly.

```text
tdw-did = "did:tdw:" *( domain-segment “.” ) scid 1*( “.” domain-segment ) ( “.” domain-segment ) *( ":" path-segment )
tdw-did = "did:tdw:" 2*( domain-segment “.” ) *( ":" path-segment ) (":" scid ) *( ":" path-segment )
domain-segment = ; A part of a domain name as defined in RFC3986, such as "example" and "com" for "example.com"
path-segment= ; A part of a URL path as defined in RFC3986, such as "path", "to", "folder" for "path/to/folder"
scid = 24( lower-base32 )
lower-base32 = [2-7a-z]
```

```example
EXAMPLE 1: Example TDW Method DIDs, and corresponding web location for the did:tdw log file

did:tdw:<SCID>.example.com
--> https://<SCID>.example.com/.well-known/didlog.txt
did:web:w3c-ccg.github.io:dids:<SCID>
--> https://example.com/dids/<SCID>/didlog.txt
did:web:<SCID>.example.com%3A3000
--> https://example.com:3000/dids/<SCID>/didlog.txt
```

The location of the `did:tdw` `didlog.txt` file is logically beside where the comparable `did:web`
`did.json` file is published. A controller **MAY** choose to publish both DIDs and so both files.

### DID Method Operations

#### Create (Register)

Creating a `did:tdw` DID is done by carrying out the following steps.

1. Define the DID string, and hence, the web location at which the DID Log (`didlog.txt`) will be published. Identify (using the placeholder `{SCID}`) where the required [[ref: SCID]] will be placed in the DID string.
2. Create the initial DIDDoc (`did.json`) file for the DID, with whatever content is required. Wherever there is self-reference to the DID in the DIDDoc, use the form defined in step 1, with the identified placeholder for the [[ref: SCID]].
   1. As per the [Authorization Keys](#authorization-keys), the DIDDoc **MUST** contain at least one `authorization` or `verificationMethod` key type.
3. Define a JSON array of valid [[ref: parameters]] that affect the generation of the DID. The [DID Generation and Validation Parameters](#parameters) section of this specification defines the permitted [[ref: parameters]].
4. Pass the DID string, initial DIDDoc, and [[ref: parameters]] to a `did:tdw` "Create" implementation that **MUST**:
   1. Calculate the [[ref: SCID]] for the DID as defined in the [SCID Generation and Validation](#scid-generation-and-validation) section of this specification.
   2. Replace in the DIDDoc the placeholder for the [[ref: SCID]] `{SCID}` with the calculated `SCID`.
   3. Generate a DID Entry as a JSON array (`[<data>]`) with the following JSON items:
      1. The [[ref: SCID]] as the `entryHash` value: `"ke465curdwjzrrp5x5ut92te"`
      2. An integer, `1`, that is the versionId for this first version of the DIDDoc: `1`
      3. A string that is the current time in [[ref: ISO8601]] format: `"2024-04-04T07:32:58Z"`
      4. The [[ref: parameters]] passed in as a JSON dict: `{"method":"did:tdw:1","scid":"en6dfezxz8yvudnyb5pq9a6g"}`
      5. The contents of the initial DIDDoc, in the form: `{"value": <DIDDoc>}`
   4. Calculate the [[ref: Entry Hash]] (`entryHash`) of the DID Entry as defined in the [Entry Hash Generation and Validation](#entry-hash-generation-and-validation) section of this specification.
   5. Update the `entryHash` with the value produced in the previous step.
   6. Generate a [[ref: Data Integrity]] proof across the entry using an authorized key from the DID, and the `entryHash` as the proof `challenge`. The definition of "authorized" in this case is specified in the [Authorization Keys](#authorization-keys) section of this specification. The proof becomes the last JSON item in the entry.
   7. Put the resulting entry, with extraneous white space removed as the contents of a file `didlog.txt` and publish the file at the appropriate location defined by the `did:tdw` value.
      1. This is a logical operation -- how a deployment serves the `didlog.txt` content is not constrained.

A controller **MAY** generate an equivalent `did:web` DIDDoc and publish it as defined in the [Publishing a Parallel `did:web` DID](#publishing-a-parallel-didweb-did) section of this specification. The `did:web` DIDDoc could be used for backwards compatibility
as a transition is made from `did:web` to `did:tdw`. Verifiers using the `did:web` lose the verifiable properties and history of the
`did:tdw` for the convenience of the simple retrieval of the `did:web` DIDDoc.

### Read (Resolve)

The following steps MUST be executed to resolve the DID document for a `did:tdw` DID:

1. Replace ":" with "/" in the method specific identifier to obtain the fully qualified domain name and optional path.
2. If the domain contains a port percent decode the colon.
3. Generate an HTTPS URL to the expected location of the DID document by prepending https://.
4. If no path has been specified in the URL, append /.well-known.
5. Append /didlog.txt to complete the URL.
6. Perform an HTTP GET request to the URL using an agent that can successfully negotiate a secure HTTPS connection, which enforces the security requirements as described in 2.6 Security and privacy considerations.
7. When performing the DNS resolution during the HTTP GET request, the client SHOULD utilize [RFC8484] in order to prevent tracking of the identity being resolved.
8. Process the [[ref: DID Log]] file as described below.

To process the retrieved [[ref: DID Log]] file, carry out the following steps:

1. Process the Log entries in the order they appear in the file, applying the [[ref: parameters]] set on current and previous entries.
2. For each entry:
   1. Update the currently active [[ref: parameters]] with the parameters from the entry. and continue processing using the active set of [[ref: parameters]].
   2. Verify that the Data Integrity proof in the entry is valid, and is signed by an authorized key as defined in the [Authorization Keys](#authorization-keys) section of this specification.
   3. Verify that the `entryHash` for the entry according to the process defined in the [Entry Hash Generation and Verification] section of this specification.
   4. For the initial version of the DIDDoc (`1`) verify that the appropriate [[ref: SCID]] is being used for the DID as defined in the [SCID Generation and Verification] section of this specification.
   5. Generate the version of the DIDDoc for the entry by using the JSON value of the `value` item, or by using [[ref: JSON Patch]] to apply the JSON value of the `patch` entry item to the previous version of the DIDDoc.
   6. If [[ref: Key Pre-Rotation]] is being used, verify that any added keys in the DIDDoc have a valid pre-rotation entry as defined in the [Key Pre-Rotation Hash Generation and Verification] section of this specification.
   7. Once each version entry has been processed, collect about each version (at least) the following information:
      1. `versionId`
      2. `versionTime`
      3. The DIDDoc

On completing the processing of the [[ref: DID Log]], respond to the DID resolution request, including the application of query parameters such as `?versionId=` and `?versionTime=` with the appropriate DIDDoc version.

The following error codes and descriptions may be returned when resolving a DID.

:::todo

Document the full list of error codes that can be generated in resolving a DID.

:::

- Code 400: The `did:tdw` DID Log file `didlog.txt` was not found.

#### Reading did:tdw DID URLs

A `did:tdw` resolver **MAY** implement the resolution of the `#whois` and a DID
URL Path using the [whois LinkedVP Service] and [DIR URL Path Resolution
Service] as defined in this specification by processing the [[ref: DID Log]] and
then [dereferencing the DID URL] using the contents of the DIDDoc. The client of
a resolver that does not implement those capabilities must use the resolver to
resolve the appropriate DIDDoc, and then process the resulting DID URLs
themselves.

### Update

To update a DID to for example, rotate a key in the DIDDoc, a new, verifiable
[[ref: DID Log Entry]] must be generated, appended to the existing [[ref: DID
Log]] (`didlog.txt`) and published to the web location defined by the DID. The
process to generate a verifiable [[ref: DID Log Entry]] follows a similar
process to the [Create](#create-register) process, as follows:

1. Make the desired changes to the DIDDoc. While the contents of a new DIDDoc version are (mostly) up to the DID controller, there are some limitations:
   1. The `id` of the DIDDoc **MAY** be changed when the DID Controller wants to (or must) publish the DID at a different location and wants to retain the [[ref: SCID]] and history of the DID. For details, see the section [Moving a DID's Web Location].
   2. If [[ref: Key Pre-Rotation]] is being used in the DID, only keys with a valid pre-rotation entry in a previous DIDDoc can be added, as defined in the [Key Pre-Rotation Hash Generation and Verification] section of this specification.
2. Define a JSON array of valid [[ref: parameters]] that affect the generation of the DID. The [DID Generation and Validation Parameters](#parameters) section of this specification defines the permitted [[ref: parameters]].
3. Pass the existing [[ref: DID Log]], the updated DIDDoc, and the [[ref: parameters]] to a `did:tdw` update implementation which **MUST**:
   1. Generate a DID Entry as a JSON array (`[<data>]`) with the following JSON items:
      1. The `entryHash` from the previous [[ref: DID Log Entry]] as the `entryHash` value.
      2. An integer that is one more than the `versionId` of the previous [[ref: DID Log Entry]].
      3. A string that is the current time in [[ref: ISO8601]] format: `"2024-04-05T07:32:58Z"`
      4. The [[ref: parameters]] passed in as a JSON dict: `{}`
         1. [[ref: parameters]] from previous versions continue to apply and do not need to be repeated in each version. As a result, the `parameters` item will often be an empty dict.
      5. Generate a [[ref: JSON Patch]] to evolve the previous DIDDoc version to the new DIDDoc version, and put the resulting patch in the item `{"patch": <DIDDoc Patch>}`. For details see the [Generating and Applying a JSON Patch].
         1. An implementation **MAY** skip the [[ref: JSON Patch]] process and simply put the full new version of the DIDDoc in the item `{"value": <DIDDoc>}` as is done in the initial entry in the log.
   2. Calculate the [[ref: Entry Hash]] (`entryHash`) of the DID Entry as defined in the [Entry Hash Generation and Validation] section of this specification.
   3. Update the `entryHash` with the value produced in the previous step.
   4. Generate a [[ref: Data Integrity]] proof across the entry using an authorized key from the DID, and the `entryHash` as the proof `challenge`. The definition of "authorized" is formalized in the [Authorization Keys](#authorization-keys) section of this specification. The proof becomes the last JSON item in the entry.
   5. Append the resulting entry to the existing contents of the [[ref: DID Log]] file `didlog.txt`.
4. Update the [[ref: DID Log]] file at the appropriate location defined by the `did:tdw` identifier.
      1. This is a logical operation -- how a deployment serves the `didlog.txt` content is not constrained.

A controller **MAY** generate an equivalent, updated `did:web` DIDDoc and publish it as defined in the [Publishing a Parallel `did:web` DID](#publishing-a-parallel-didweb-did) section of this specification.

#### Deactivate (Revoke)

To delete the DID document, the the file `didlog.txt` has to be removed or has to be no longer publicly available due to any other means.

:::todo

Add in methods to deactive the DID while still making it resolvable.

:::

### DID Method Processes

#### DID Generation and Validation Parameters

:::todo

Complete this section.

:::

#### SCID Generation and Validation

:::todo

Complete this section.

:::

 `left(base32_lower(hash(JCS(initial DIDDoc))), 24)`
      1. `left` extracts the defined number of characters (24) from the string.
      2. `base32_lower` as defined by [[ref: base32_lower]].
      3. `hash` is either [sha256] or an alternative hash algorithm defined in the `hash` item in the [[ref: parameters]].
      4. `JCS` is an implementation of the [[ref: JSON Canonicalization Scheme]].

#### Entry Hash Generation and Validation

Calculate the entryHash of the DID Entry as base32_lower(hash(JCS(entry))), where base32_lower, hash and JCS are the same functions used for generating the SCID (above).

#### Authorization Keys

Each entry in the [[ref: DID Log]] MUST include a [[ref: Data Integrity]] proof signed by a key **authorized** to control (create, update, deactive) the DID. For `did:tdw`, the following defines the process for collecting the authorized keys.

1. Retrieve the DIDDoc in which the set of authorized controller DIDs is found. For the first version (`1`) of the DID, that is the first (and only) DIDDoc. For all subsequent versions of the DID, the **previous** DIDDoc version is used.
2. From the DIDDoc, the top-level `controller` item is retrieved to create a (possibly empty) array of controller DIDs from the DIDDoc.
   1. If the list of controller DIDs is empty, the DID being signed is added to the array.
3. For each DID in the list, the set of `authentication` key type references are collected from within the DIDDoc.
   1. If there are no `authentication` key type references, the `verificationMethod` key references are collected.
   2. If the controller DID is for an **external** DID, the key references **MUST** be present in the DIDDoc being processed.

The controller of the DID **MUST** use a key from the resulting key references to sign the [[ref: DID Log]] entry.

A resolver of the DID **MUST** verify that the key used for signing the [[ref: DID Log]] entry is in the list of authorized DID key references, and **MUST** verify the proof.

The following is some non-normative background on the process listed above:

- The [[ref: DID Core Specification]] is not clear (at least to the authors of this specification) on what key types define those authorized to update a DID.
- The requirement to have the key reference for external DIDs (not the controlled DID) copied into the DIDDoc is to prevent an implementation from having to resolve external DIDs (that could use any [[ref: DID Method]]) during the resolution of a DID. This *might* be too restrictive and could be changed in an update to this specification. For example, it might be reasonable to require that external DIDs of certain [[ref: DID Methods]] (such as `did:tdw` or `did:web`) be resolved as part of resolving the controlled DID.
- In a future version of the specification, the authors would like to require support for [[ref: verifiableConditions]] key types, to enable [[ref: multi-sig]] DID control support, such as requiring "N of M" signatures must be in a proof for it to be valid.

#### Publishing a Parallel `did:web` DID

:::todo

Update this section.

:::


#### Generating and Applying a JSON Patch

:::todo

Update this section.

:::