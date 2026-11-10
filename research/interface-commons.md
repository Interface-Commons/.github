# Interface Commons

> This repository is a bridge document. Interface Commons lives at its own
> GitHub presence under the Open Commons organisation. This file explains how
> Interface Commons relates to the Open Commons methodology and the master board.
>
> **Primary repository:** [interface-commons on GitHub](https://github.com/opencommons/interface-commons)
> **Vision document:** See the full OpenHIG Vision Document in the primary repository.

---

## What Interface Commons is

Interface Commons is a conceptual framework and ecosystem coordination project for
human interface protocols. It is platform-agnostic and toolkit-neutral. Its primary
deliverable is **OpenHIG** — an open Human Interface Guidelines document that any
application, on any shell, on any form factor, can voluntarily build from.

It operates the same methodology as every Open Commons project: prior art analysis,
named concepts, gap and overlap mapping, and an Observatory that tracks ecosystem
progress and provides coordination infrastructure.

---

## How it relates to Open Handset Commons

Interface Commons and Open Handset Commons are independent. Interface Commons has no
dependency on Open Handset Commons. It is not a sub-project of open handsets — it is
a general framework for interface protocol coordination that applies to desktops,
tablets, TVs, and form factors not yet named.

Open Handset Commons *draws from* Interface Commons: a complete open handset requires
a coherent interface layer, and Interface Commons is where that work is being coordinated.
But the relationship runs one way. Interface Commons does not need to know about the
Radio Wall or the Two Minds to do its work.

---

## Scope of Interface Commons

Three intersecting layers:

**The app layer** — how applications structure their UI, expose navigation state, declare
layout capabilities, and respond to context signals from their environment.

**The shell layer** — how shells (Phosh, GNOME, KDE Plasma, sway) communicate context to
apps, and how they optionally consume structured information apps expose.

**The interface layer** — the boundary between app and shell as a negotiation surface.
Input methods and output constraints treated as a unified problem, not separate concerns.

---

## Prior art tracked by Interface Commons

*(To be populated as Interface Commons' research and consolidation phase completes.
See the primary repository for the current state of the prior art catalogue.)*

Key prior art already identified in the vision document:
- GNOME HIG and libadwaita breakpoints
- KDE HIG and Kirigami adaptive layouts
- Apple HIG
- Google Material Design
- freedesktop.org / XDG specs
- Wayland protocol extensions (xdg-shell, text-input)
- XDG Portals
- MPRIS
- WAI-ARIA (as a model for retrofitting semantic contracts)

---

## Interface Commons on the master board

Interface Commons' tracked projects and concept maturity ratings appear in the master
board once the OpenHIG conceptual model is formalised. The concept columns for the
Interface Commons section will be added at that point.
