# Trust DID Web Work Item Rolling Agenda<!-- omit in toc -->

Zoom Link: [https://us02web.zoom.us/j/83119969275?pwd=IZTuXgGLtdLPjPLuB6q8zHXazxHSsU.1](https://us02web.zoom.us/j/83119969275?pwd=IZTuXgGLtdLPjPLuB6q8zHXazxHSsU.1)

Agenda: [HackMD](https://hackmd.io/k4cIK9vQSlaeg2pdHE51IQ), [TrustDIDWeb Repository](https://github.com/decentralized-identity/trustdidweb/blob/main/agenda.md) (synchronized after each meeting)

[**WG projects**](https://github.com/decentralized-identity?q=wg-cc&type=&language=) | [DIF page](https://identity.foundation/working-groups/claims-credentials.html) | [Mailing list and Wiki](https://lists.identity.foundation/g/cc-wg) | [Meeting recordings](https://docs.google.com/spreadsheets/d/1wgccmMvIImx30qVE9GhRKWWv3vmL2ZyUauuKx3IfRmA/edit?gid=111226877#gid=111226877)

## Table of Contents<!-- omit in toc -->

- [Meeting Information](#meeting-information)
- [Future Topics](#future-topics)
- [Meeting - 12 Sept 2024](#meeting---12-sept-2024)

## Meeting Information

- Before you contribute - **[join DIF]** and [sign the WG charter] (both are required!)
- Meeting Time: Every second Thursday at 9:00 Pacific / 18:00 Central Europe
- [Calendar entry]
- [ID WG participation tracking]
- [Zoom room]
- Links and Repositories:
    - [Specification], [Spec Repository](https://github.com/decentralized-identity/trustdidweb)
    - Implementations: [TS](https://github.com/decentralized-identity/trustdidweb-ts), [Python](https://github.com/bcgov/trustdidweb-py), [Go](https://pkg.go.dev/github.com/nuts-foundation/trustdidweb-go)
    - Trust DID Web Server

_Participants are encouraged to turn your video on. This is a good way to build rapport across the contributor community._

_This document is live-edited DURING each call, and stable/authoritative copies live on our github repo under `/agenda.md`, link: [Agenda]._

[join DIF]: https://identity.foundation/join
[sign the WG charter]: https://bit.ly/DIF-WG-select1
[Calendar entry]: https://calendar.google.com/event?action=TEMPLATE&tmeid=NG5jYWowbmZsdWNzM21tYjBsbDIzdG50ZzFfMjAyNDA5MTJUMTYwMDAwWiBkZWNlbnRyYWxpemVkLmlkZW50aXR5QG0&tmsrc=decentralized.identity%40gmail.com&scp=ALL
[Zoom Room]: https://us02web.zoom.us/j/83119969275?pwd=IZTuXgGLtdLPjPLuB6q8zHXazxHSsU.1
[DIF Code of Conduct]: https://github.com/decentralized-identity/org/blob/master/code-of-conduct.md
[ID WG participation tracking]: https://docs.google.com/spreadsheets/d/12hFa574v5PRrKfzIKMgDTjxuU6lvtBhrmLspfKkN4oE/edit#gid=0
[operations@identity.foundation]: mailto:operations@identity.foundation
[did:tdw Specification license]: https://github.com/decentralized-identity/trustdidweb/blob/main/LICENSE.md
[Agenda]: https://github.com/decentralized-identity/trustdidweb/blob/main/agenda.md
[Specification]: https://identity.foundation/trustdidweb

## Future Topics

- Using the `did:tdw` log format with other DID Methods
- Merging `did:tdw` features into `did:web`?
- Implementor's experiences -- architectures, learnings
- Trust DID Web Server -- implementations, [such as this one](https://github.com/decentralized-identity/trustdidweb-server-py), specification
- A did:tdw test suite -- such as proposed [here](https://github.com/nuts-foundation/trustdidweb-go/pull/1)

## Meeting - 12 Sept 2024

Time: 9:00 Pacific / 18:00 Central Europe

Meeting Recording: [Zoom Recording](https://us02web.zoom.us/rec/share/-tz_UHUxqNxkGntAcYZEaYD1_EDX4RBVmtwd7JbGKFglgwTYzJUzkC2ZuFRFZftt.-wWj9ZMqS70V8Cwg)

Attendees:

* Stephen Curran
* Dmitri Zagidulin
* Cole Davis
* Brian Richter
* Andrew Whitehead
* Sylvain Martel
* Martina Kolpondinos
* John Jordan
* Patrick St. Louis

1. Welcome and Adminstrivia
    1. Recording on?
    2. Please make sure you: [join DIF], [sign the WG Charter], and follow the [DIF Code of Conduct]. Questions? Please contact [operations@identity.foundation].
    3. [did:tdw Specification license] -- W3C Mode
    4. Introductions and Agenda Topics
2. Introduction to the `did:tdw` Work Item at DIF
    1. [CCG Presentation on did:tdw](https://meet.w3c-ccg.org/archives/w3c-ccg-weekly-2024-07-09.mp4) (starts at the 5:40 mark of recording)
3. Brief(!) introduction to `did:tdw`
4. Discussion:
    1. What do you want this group to achieve?
    2. What would help you the most?
        1. Get to 1.0!
        2. Web server
        3. Next step topics -- witnesses, deactivation -- how does a diploma remain verifiable when the isssuer disappears -- with their web server.  Aka durability.
        4. Acceptance of the method broadly.
        5. How `did:tdw` compares with KERI.
        6. Test suite!!!!! Implementation consistency.
        7. Cryptographic audit on the techniques used -- hashing use, etc.
        8. Governemnt acceptance of the cryptographic suites being used.
        9. Switchcord is running live use cases based on `did:web` -- would like to transition to `did:tdw` and its features.
5. Feature list [feedback document](https://docs.google.com/document/d/1jaKy0KbImVplW7xl2jMzI_MgayMQbI2o8TI6ZTvWHso/edit?usp=sharing) -- importance of features?
6. Future Topics
7. Next Meeting -- next week, same time
    1. Input to TPAC.
8. [Spec. PRs and Issues](https://github.com/decentralized-identity/trustdidweb)
9. Action items and next steps:
    1. Stephen to create a PR to change the spec. to say that a version is an object, JSON Patch is no longer used, and that the Data Integrity Proof is across the version object, without a challenge.
    2. Everyone to look at the [list of did:tdw features](https://docs.google.com/document/d/1jaKy0KbImVplW7xl2jMzI_MgayMQbI2o8TI6ZTvWHso/edit?usp=sharing) and comment on the features.
    3. Everyone to review issues and open others as needed, to drive future discussions.
