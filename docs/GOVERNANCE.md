# Governance & safety model

> Beta preview. This is the design philosophy, stated at a level that gives nothing
> weaponizable away. The enforcement code is not part of this public repository.

Cyber Umbra is **semi-autonomous, not autonomous**. The whole design exists to let a human
expert move faster *without* handing consequential decisions to a machine. The safety
properties below are meant to be structural — enforced by the system — not promises made
in documentation.

## Two human gates

1. **Engagement gate** — nothing begins until a human confirms an authorized, scoped
   engagement. Scope is explicit and checked.
2. **Action gate** — any step beyond passive analysis requires a human authorization.
   Higher-impact actions are authorized more narrowly, and exploitation-level actions are
   authorized per action, never in bulk.

## Core invariants

- **Authorized only.** The system is for engagements with explicit written authorization,
  confined to the agreed scope.
- **Analysis-first.** The system maps and reasons before it touches a target actively.
  Passive precedes active; anonymous precedes authenticated.
- **Candidate ≠ confirmed.** A knowledge match, a version lead, or a reflected input is a
  *candidate*. Confirmation requires human-reviewed evidence.
- **ML never auto-confirms.** Machine learning ranks and suggests; it never promotes a
  finding to confirmed by itself.
- **Ingested content is data, not instructions.** Nothing read from a corpus or a target
  can redirect the system's behavior.
- **Bounded by construction.** Active work runs under explicit, positive limits
  (what, where, how much), and stops when they are reached.
- **The agent does not escalate itself.** It cannot grant itself authority, widen its own
  scope, or publish its own results.

## Why publish the governance and not the engine

The governance model is the part worth sharing: it shows how to build offensive-security
automation **responsibly**. The engine, the models, and anything that lowers the barrier
to misuse stay private. A public preview should demonstrate maturity, not distribute
capability.
