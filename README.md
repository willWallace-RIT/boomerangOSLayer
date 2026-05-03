Boomerang: Context Switching Layer for Operating Systems

Overview

Boomerang is a GUI-level context switching system built on top of snapshot-based application state.

Instead of traditional multitasking (background processes), Boomerang introduces:

«A focus-driven system where inactive applications are replaced by snapshots and instantly restored when revisited.»

---

Core Idea

Every application exists in one of two states:

1. Active (Live)
   
   - Fully running
   - Interactive

2. Boomerang State (Snapshot)
   
   - Execution suspended
   - Replaced by a visual snapshot
   - Consumes near-zero resources

---

The "Boomerang" Mechanism

When switching between applications:

[App A Active]
      ↓ switch
[Capture A → Snapshot]
      ↓
[Enter Boomerang Layer]
      ↓
[Restore App B]

The "boomerang" is the intermediary layer that:

- Handles capture/restore transitions
- Manages state storage
- Provides visual continuity

---

UI/UX Model

Snapshot Windows

- Each inactive window becomes a static screenshot
- Appears identical to its last state
- No live computation behind it

Instant Restoration

- Clicking a snapshot:
  - Triggers restore
  - Replaces image with live app seamlessly

---

Design Goals

1. Zero Background Overhead

No idle CPU/RAM usage for inactive apps.

2. Seamless Illusion

User perceives continuous state despite full suspension.

3. Deterministic Focus

Only one (or few) apps truly exist at runtime.

4. OS-Agnostic Integration

Can be layered onto existing desktop environments.

---

Architecture

Components

1. Snapshot Engine (USE)

- Handles capture/restore

2. Boomerang Manager

- Tracks active/inactive states
- Orchestrates transitions

3. Window Proxy Layer

- Displays snapshot images
- Intercepts user interaction

4. Transition Renderer

- Animates switching (optional but important for UX)

---

State Flow

ACTIVE → (switch out)
    ↓
CAPTURE → SNAPSHOT STORED
    ↓
WINDOW BECOMES STATIC IMAGE

USER RETURNS
    ↓
RESTORE SNAPSHOT
    ↓
LIVE PROCESS RESUMES

---

Key Innovations

Visual Persistence Without Execution

Users see everything, but almost nothing is running.

Focus as a First-Class Primitive

The OS revolves around attention, not processes.

Modular OS Feature

- Could integrate into:
  - Linux window managers
  - Wayland compositors
  - Experimental shells

---

Technical Considerations

Snapshot Latency

- Must feel instant (<100ms target)

GPU / Rendering State

- Need to reconstruct graphical context

Input Buffering

- Prevent input during restore phase

Compatibility Modes

- Fallback for unsupported apps (keep running)

---

Example Workflow

1. User working in browser
2. Switches to IDE
3. Browser:
   - Snapshot taken
   - Fully unloaded
4. IDE restored instantly
5. Switching back:
   - IDE snapshot
   - Browser restored exactly where it was

---

Potential Extensions

- Multi-state history (time travel)
- Predictive preloading
- Collaborative shared snapshots
- Cloud-synced state

---

Comparison to Existing Models

Model| Resource Usage| State Fidelity| Speed
Background Apps| High| Medium| Instant
Hibernation| Low| High| Slow
Boomerang| Near Zero| High| Near Instant

---

Roadmap

- [ ] Build snapshot-backed window manager prototype
- [ ] Integrate with Wayland compositor
- [ ] Implement snapshot preview system
- [ ] Optimize restore latency
- [ ] UX testing for perceived continuity

---

Philosophy

Boomerang redefines multitasking:

«Not "many things running at once"
but "one thing fully alive, everything else perfectly paused"»

---

Status

Concept / Prototype Design

Looking for:

- Linux graphics/Wayland developers
- Systems engineers
- UX designers focused on perception & latency

---
