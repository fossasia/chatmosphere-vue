# eventyay-flowspace

**eventyay-flowspace** is a planned spatial video lounge component for Eventyay.
It is designed to provide informal, hallway-style interaction for online and hybrid events, where participants can move freely in a shared space and audio volume adapts based on proximity.

This project is inspired by Chatmosphere, but is a **new implementation** built for modern web technologies, current Jitsi versions, and deep integration with Eventyay. The original Chatmosphere project is no longer actively maintained, and Flowspace aims to address this gap with a sustainable and extensible approach.

## Project status

This project is **in the design and planning phase**.

The repository will initially focus on:

* architecture decisions
* integration contracts
* deployment strategy
* contributor onboarding
* incremental implementation milestones

No stable releases or production-ready builds exist yet.

## Motivation

Online conferences lack the informal social spaces that naturally exist at in-person events: hallway conversations, spontaneous meetups, and casual networking.

Traditional video conferencing tools are optimized for structured meetings, not for fluid, participant-driven interaction.

Flowspace aims to:

* recreate informal social dynamics in online events
* integrate naturally into Eventyay’s event and room model
* remain fully open source and self-hostable
* avoid reliance on outdated or unmaintained codebases

## Core idea

Flowspace provides a **spatial video experience**:

* Participants appear in a shared 2D space
* Users can move freely
* Audio volume changes based on distance
* Small group conversations emerge naturally
* No explicit breakout rooms are required

This experience complements, rather than replaces, traditional session rooms.

## Integration with Eventyay

Flowspace is designed as an **external application** that integrates tightly with Eventyay via APIs.

Eventyay acts as the **control plane**:

* user authentication
* access control
* role management
* room configuration
* nickname or display name policies

Flowspace acts as the **interaction layer**:

* spatial UI
* proximity logic
* audio handling
* real-time presence

Jitsi acts as the **media plane**:

* audio and video transport
* signaling
* optional server-side access enforcement

This separation keeps Flowspace reusable while ensuring Eventyay remains authoritative.

## Planned use cases

Within a single Eventyay event, organizers should be able to offer:

* **Spatial lounge rooms**
  Informal networking and social interaction using Flowspace

* **Workshop or session rooms**
  Structured meetings using the standard Jitsi Meet interface

Both room types can run on the same Jitsi deployment while providing very different user experiences.

## Technology direction

The following choices reflect **intent and design direction**, not final implementation guarantees.

### Frontend

* Vue.js (Vue 3)
* TypeScript
* Modern build tooling (for example Vite)

### Media

* Jitsi via lib-jitsi-meet
* Per-participant audio control
* Web Audio API for proximity-based attenuation

The Jitsi iframe API is intentionally not sufficient, because real proximity audio requires direct access to individual audio streams.

### Deployment

* Docker and Docker Compose
* Single-VM friendly
* No Kubernetes requirement
* Pinned Jitsi versions for stability

The goal is reproducible, automated deployments without operational complexity.

## Identity and nicknames

Flowspace will not manage user accounts.

Instead:

* Eventyay provides the display name or nickname
* Logged-in users are automatically identified
* Policies such as rename restrictions are enforced by configuration
* Optional guest access can be supported, but is not required

This ensures consistency across Eventyay sessions and lounges.

## Security model (planned)

* Eventyay authorizes access before joining Flowspace
* Optional JWT-based access enforcement on the Jitsi server
* Short-lived join tokens
* No reliance on obscurity of room URLs

Security is considered part of the core design, not an afterthought.

## Development approach

The project is expected to evolve in stages:

1. Architecture definition and API contracts
2. Minimal spatial UI and movement
3. Jitsi integration with proximity audio
4. Eventyay join flow and identity handling
5. Automated Docker-based deployment
6. Iterative refinement and feature expansion

The emphasis is on **clarity, maintainability, and incremental progress**, not on rapid prototyping.

## Relationship to Chatmosphere

Chatmosphere demonstrated the value of spatial video chat, but:

* it targets older Jitsi versions
* it bundles dependencies in ways that are difficult to upgrade
* it is no longer under active development

Flowspace does not fork Chatmosphere.
It treats Chatmosphere as **conceptual inspiration**, not as a technical base.

## Target audience

* Event organizers using Eventyay
* Open source conference communities
* Contributors interested in real-time web applications
* GSoC contributors looking for a well-scoped but non-trivial project

## Contributing

At this stage, contributions are expected to focus on:

* architecture discussions
* API design
* documentation
* proof-of-concept components

As implementation progresses, contribution guidelines will be expanded.

## License

This project is intended to be released under the Apache2 License compatible with Eventyay and the wider FOSSASIA ecosystem.
