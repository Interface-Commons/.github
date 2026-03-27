# Interface Commons
### The OpenHIG Project — Vision Document

> *"Coordination is achieved not by authoritative orders, but by finding and highlighting needs — and providing concrete means to fill them."*

---

## On the Name

**Interface Commons** is the project.
**OpenHIG** is the specification it produces — the open Human Interface Guidelines document, platform-agnostic and community-owned.

The separation is intentional. A commons is shared infrastructure: it belongs to everyone who uses it and no one who controls it. The guidelines that emerge from it are a deliverable, not a decree. The project name reflects what this is. The spec name reflects what it produces.

**OpenHIG** is clear — no existing project occupies the name. It is precise and immediately legible. Where Apple's HIG is a platform-specific rulebook for one ecosystem, OpenHIG is a voluntary, cross-platform reference for any ecosystem. The contrast is the point.

---

## What This Is

A community coordination project and open reference framework with one goal:
**establish a shared, platform-agnostic vocabulary of human interface principles and protocols** — so that any application, on any shell, on any form factor, has a clear, citable, optional foundation to build from.

This is not a toolkit. Not a fork. Not a new shell. Not a design system.
It is a **living framework** — principles for *why*, protocols for *how*, and a visual demonstration engine that makes both tangible, testable, and formally consistent without writing a line of code.

---

## Scope: Broader Than Mobile, Deeper Than Apps

This project is not exclusively about mobile Linux. Mobile Linux is the origin story — the concrete, urgent, underserved problem that makes the need visible. But the framework it produces is universal.

**The scope covers three intersecting layers:**

**1. The app layer**
How applications structure their UI, expose their navigation state, declare their layout capabilities, and respond to context signals from the environment they run in.

**2. The shell layer**
How shells (GNOME, KDE Plasma, Phosh, sway, and others) communicate context to apps — form factor, input method, available screen area, safe zones — and how they can optionally consume structured information that apps expose.

**3. The interface layer — input and output as one**
The boundary between app and shell is not a wall. It is a negotiation surface. The framework treats input methods (touch, pointer, keyboard, gesture) and output constraints (screen size, orientation, notch, gesture zones) as a **unified problem** — not separate concerns handled by separate specs. Flows that cross this boundary are first-class protocol territory, not edge cases:
- A virtual keyboard appearing mid-task and shrinking usable area
- A back gesture intercepted by the shell vs. consumed by the app
- A menu list migrating from inside the app to the shell's drawer
- An app reforming its layout as the device rotates or the window narrows

---

## Why This Needs to Exist

Linux now runs on aarch64 handsets via postmarketOS and similar distributions. The hardware problem is largely solved. The software problem isn't.

Major open-source desktop applications — GIMP, Inkscape, VLC, Audacity, LibreOffice, and hundreds of others — were designed for mouse, keyboard, and large screens. Most of them have no touch target sizing awareness, rely on hover states that don't exist on touchscreens, break in portrait orientation, and have never received a single issue or PR framing handsets as a use case.

The GNOME and KDE ecosystems have done significant work on adaptiveness — but within their own toolkits, for their own apps. Nobody is doing this **cross-ecosystem, toolkit-agnostic, and at scale**.

Beyond Linux mobile, the same gap exists everywhere. Apple has the HIG. Google has Material. Both are platform-specific, proprietary in spirit, designed to produce conformity within their own ecosystems. The open-source world has excellent fragments — but no synthesis, and no neutral ground.

The gaps are:
1. No shared vocabulary for what "interface-aware" means outside of one platform
2. No coordination layer connecting contributors to where effort is needed
3. No neutral reference that maintainers can cite when accepting or rejecting patches
4. No visual, formally consistent demonstration of what the protocols actually *do*

---

## What This Is Not

- **Not a mandate.** Every application can still do whatever it wants with its UI.
- **Not a new toolkit or widget library.** We work with GTK, Qt, Flutter, and others as they are.
- **Not a design system.** This framework does not dictate colors, typography, or visual language.
- **Not limited to phones.** The same principles apply to tablets, tiling WM users, TV interfaces, convertibles, and form factors not yet named.
- **Not a fork.** All work is directed upstream.
- **Not GNOME. Not KDE. Not anyone's.** Existing ecosystem work is research input, not authority.

---

## How Coordination Works Here

This project does not coordinate by authority. It coordinates by **clarity**.

The mechanism:
1. Find a real, unmet need in the interface layer
2. Research what already exists that addresses it — fully, partially, or not at all
3. Document the need in concrete, human terms
4. Propose a protocol — optional, named, scoped, behavior-defined
5. Demonstrate it in the engine, which checks it against all existing protocols for consistency
6. Open well-formed, citable issues in upstream projects
7. Track what happens

Anyone who sees the need and has the capacity can pick up any part of this. The project's job is to make the need visible and the path concrete — not to own the outcome.

---

## Project Structure

Five layers, each a distinct subproject with its own deliverables.

---

### Layer 1 — Research & Consolidation
**Status: First subproject. Starting point.**

Before writing a single new principle or protocol, map everything that already exists.

**Scope:**
- All existing Human Interface Guidelines: GNOME HIG, KDE HIG, Apple HIG, Google Material Design, Microsoft Fluent Design, and others
- All existing technical protocols relevant to app–shell interaction on Linux: freedesktop.org / XDG specs, Wayland protocol extensions (xdg-shell, text-input, xdg-decoration), D-Bus interfaces, AppStream/Flatpak metadata, MPRIS
- Mobile-specific existing work: postmarketOS/Phosh adaptation efforts, Libadwaita breakpoints, Kirigami adaptive layouts, Android back stack model, iOS safe area / inset protocols, Android input method protocols

**Output:**
- A structured index of all existing specs, guidelines, and protocols
- A categorization by layer: principle vs. protocol vs. implementation detail
- A gap map: interaction scenarios with no existing protocol
- An overlap map: where existing standards conflict or duplicate

**Key question:** *What has already been solved, what has been partially solved, and what is genuinely missing?*

---

### Layer 2 — Principles (The OpenHIG)
**The why.**

A platform-agnostic, toolkit-neutral human UI philosophy, synthesized from the research layer. The underlying reasoning that makes a UI work for humans across form factors and input methods.

Covers things like:
- Why minimum touch target size exists and what it should be
- Why hover-only interactions are an exclusion pattern, not just a mobile problem
- Why portrait and landscape are both valid primary orientations
- Why virtual keyboard awareness is a contract between app and environment
- Why "responsive" is not the same as "adaptive"
- Why the boundary between input and output is a negotiation surface, not a wall
- Why app menus, navigation history, and window chrome are shell concerns as much as app concerns

**Output:** A human-readable principles document. Concise. Citable. Designed to be linked in upstream issues as shared reasoning — not as authority, but as vocabulary. This document is the OpenHIG.

---

### Layer 3 — Protocols
**The how.**

Concrete, optional, interoperable contracts between applications and shells. Each protocol is:
- **Named and versioned**
- **Clearly scoped** — what problem it solves and what it explicitly does not
- **Defined by behavior, not implementation** — realizable in GTK, Qt, or anything else
- **Adoption-optional** — implementing zero protocols is valid; implementing one is progress
- **Described in a unified structured YAML format** — consumed by the demonstration engine automatically

**Example protocols:**

| Protocol | Layer | Description |
|---|---|---|
| `back-navigation` | App → Shell | App declares internal navigation history; shell provides back signal; app decides whether to consume it |
| `app-menu-offload` | App → Shell | App exposes structured menu tree; shell may display it natively (global bar, swipe drawer, or ignore) |
| `vkb-negotiate` | App ↔ Shell | App signals keyboard intent; shell confirms and communicates usable screen area after keyboard appears |
| `touch-intent` | App ↔ Shell | App declares touch-optimized mode; shell may request activation based on detected input context |
| `portrait-hint` | App → Shell | App declares portrait layout support; shell may prefer this orientation |
| `safe-area-inset` | Shell → App | Shell communicates unusable regions (notch, gesture zones, corners); app adjusts layout |
| `layout-context` | Shell → App | Shell communicates form factor (handset, tablet, desktop, tiling); app may adapt layout |
| `input-method-context` | Shell → App | Shell communicates primary input (touch, pointer, stylus, keyboard); app may adapt interaction |

Each protocol is a **building block**, not a system. Apps and shells adopt what makes sense for them.

---

### Layer 4 — The Demonstration Engine
**The living specification — and the consistency layer.**

A visual, interactive UI constructor that demonstrates all protocols in real time. Not a mockup. A working reference environment that also serves as a **formal consistency enforcer**.

**What it shows:**

- An abstract application running inside an abstract shell
- Form factor switching: handset portrait, handset landscape, tablet, desktop, tiling
- Input method switching: touch, pointer, keyboard
- All active protocols visible — when a protocol fires, the relevant contract is highlighted and explained inline
- Protocol behavior in action:
  - `back-navigation` — in-app history slides back as the shell's back gesture fires
  - `app-menu-offload` — menu clears from inside the app and surfaces in the shell's bar or drawer
  - `vkb-negotiate` — keyboard appears, usable area shrinks, app repositions its active input
  - `safe-area-inset` — notch and gesture zones appear, layout reflows away from them
- Protocols can be toggled on and off to compare behavior with and without each contract

**How protocols get added:**

Each protocol is a YAML file in the repository. When a contributor adds one, CI rebuilds the engine automatically. The protocol appears in the engine with its behavior demonstrated — **zero coding knowledge required from the protocol author**. The engine serves as guide, registry, cookbook, and demonstration stand simultaneously.

**The consistency enforcement role:**

When a new protocol YAML is submitted, the engine does more than render it. It checks the new protocol against the full existing set:

- **Overlap detection:** Does this protocol claim a signal or behavior already owned by another? Two protocols cannot both be the authoritative handler of the back gesture without explicitly declaring a priority relationship.
- **Contradiction detection:** Does this protocol produce a state that is logically incompatible with another active protocol? Can both be active simultaneously, and if so, what happens?
- **Uncovered flow detection:** As the protocol space grows, the engine can surface interaction scenarios that no protocol addresses — not as proof that something is *wrong*, but as a signal that a gap *may exist* and is worth examining.

This is not a claim to completeness. There is no absolute UI against which gaps can be definitively measured. But a formally consistent, internally non-contradictory protocol space is an achievable and meaningful target — and the engine is the instrument that keeps it honest.

**The deeper implication:**

The engine is a form of **meta-bootstrap** — an abstract UI reference implementation not tied to any specific toolkit, rendering technology, or platform. The same YAML protocol definitions that drive the engine can inform implementation in GTK, Qt, WPF, HTML/CSS, Flutter, or anything else. The protocol is the truth. The engine makes it visible and keeps it consistent. Toolkit implementations are consequences.

This is the closest the project comes to the concept of an *absolute interface* — not a claim that the complete set of UI contracts can ever be fully known, but a commitment to building a space that is internally coherent, formally testable, and as complete as the community can collectively make it.

---

### Layer 5 — Adoption Interface
**The coordination layer.**

**App and shell tracker:**
A structured, public list of major open-source applications and shells with adoption status across relevant protocols. Updated automatically via CI from upstream issue trackers.

Columns per app: *issue opened → acknowledged → in progress → merged → released*

**Issue templates:**
Standardized, protocol-linked feature request templates. Each references the relevant protocol, links to the OpenHIG for rationale, and defines concrete acceptance criteria — so maintainers know exactly what "done" looks like before they start.

**Contribution guide:**
How anyone can pick an app from the tracker, open a well-formed issue, and contribute — without being an expert in mobile UI or the app's codebase.

**Impact log:**
A visible record of what has actually been merged and shipped. The social proof layer — it makes saying *"no"* to the next maintainer feel like being left behind.

---

## The Role This Project Needs

Not primarily a development effort. A **coordination and clarity effort**.

The core role: the person who shows up consistently, writes the doc nobody wrote, structures the problem nobody structured, and connects the people who should have talked three weeks ago.

Specific responsibilities:
- Maintaining vision and scope documents
- Owning the research and consolidation phase
- Drafting and iterating the OpenHIG
- Designing the protocol YAML format and engine integration contract
- Opening and tracking upstream issues
- Coordinating contributors across apps, shells, and the engine
- Communicating progress publicly
- Writing grant proposals to NLnet, GNOME Foundation, KDE e.V. as the project matures

This role does not require being the best developer in the room.
It requires being the person who ensures everyone else has clarity about what they're building, for whom, and why.

---

## On Legitimacy

Nobody appointed this project. Nobody approved it. There is no committee that grants the authority to start coordinating something that needs coordinating.

That is, in fact, how most useful things in open source begin.

The correct question is not *"who gave you the right?"* — it is *"is this work needed, and is it being done well?"* If the answer to both is yes, the project earns its place by existing and delivering.

If someone else can do it better — great. This project will link to their work, say thank you, and consider the problem solved.

The goal was never ownership. It was to make sure the work gets done.

---

## Known Risk: The Standards Graveyard

There is a long history of failed "universal UI standard" attempts. Most failed by trying to be prescriptive.

This project avoids that failure mode by design:
- **Zero mandates.** Every protocol is opt-in.
- **No new shell, no new toolkit.** We work within existing ecosystems.
- **Vocabulary first.** The goal is to become the shared language people reach for when they want consensus — not the law they're subject to.
- **Show, don't tell.** The engine makes protocols tangible before any implementation exists.
- **Formally honest.** The engine's consistency checking means the project cannot accidentally produce contradictory standards without detecting it. That's structural protection against the kind of incoherence that kills standards efforts.
- **Incremental proof.** Each merged patch is a public proof of concept. The project earns legitimacy by shipping, not by declaring.

---

## Immediate Next Steps

1. **Establish home** — Public GitLab or GitHub presence under the Interface Commons name
2. **Subproject 1 kickoff** — Research and consolidation phase; structured intake of existing HIGs and protocol specs
3. **Protocol YAML format** — Design the unified structured format that feeds the engine
4. **Publish this document** — As the project's public-facing README
5. **First outreach** — 2–3 high-visibility apps as initial targets; open well-formed proof-of-concept issues
6. **Community anchor** — postmarketOS Matrix, GNOME Discourse, KDE forums

---

## Related Prior Art to Study

- **freedesktop.org** — The model for neutral, cross-desktop Linux protocol coordination
- **MPRIS** — A successful optional, widely-adopted D-Bus protocol: the pattern this project generalizes
- **WAI-ARIA** — Retrofitting semantic contracts into existing software without forking it
- **Wayland text-input protocol** — Already solves part of vkb-negotiate; build on it, not around it
- **XDG Portals** — A model for app–shell capability negotiation
- **GNOME Mobile initiative** — The closest existing effort; defines one boundary of what this project is not

---

*This document is a living draft. It will be updated as the research phase produces findings and as the founding community shapes the project's direction.*
