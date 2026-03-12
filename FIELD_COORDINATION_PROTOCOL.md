# Field Coordination Protocol
### How to Use the KindField Coordination Engine — A Practitioner's Guide

*Version 1.0 — March 2026*

---

## Who This Is For

This document is for practitioners, community members, and participants working in any KindPath field. You don't need to understand the technical architecture to use this guide. You need to understand the principles — which aren't complicated, because they're borrowed from how living systems actually work.

If you've gardened, raised children, maintained a long friendship, cared for land, or been part of a functioning community — you already understand this. This document just names it in a way that the software can work with.

---

## The Central Idea

Work in a conventional system flows:
> Task gets created → assigned to someone → worked on → reviewed → approved → closed → forgotten

Work in the KindField engine deposits:
> Participant notices something needs contributing → makes a contribution when capable → contribution rings in the field permanently → field responds → deposit enriches the archive that future contributions build on

The key differences:
- **You are never assigned.** Work is not distributed to you like mail. You bring work to a field because you are enrolled in that field and the work is yours to make.
- **Nothing is discarded.** Not the completed work, not the context that didn't fit, not the divergent response.
- **Nothing is approved.** Work either resonates with the field or it diverges from it. Divergence is not failure. It is signal.
- **Time is yours.** Work happens when your biological state supports it, not when a deadline demands it.

---

## How to Use a Field

### What a field is

A field is a relational zone where related work accumulates over time. It has a name, a purpose, and a sense of what it values (governed by its KindEarth pillar weights). It has a steward — someone who tends the field's health without controlling it.

Examples of fields:
- The NDIS care coordination field
- The DFTE trading architecture field
- The community ecological observation field
- The KindPath canon development field
- The Northern Rivers practitioners field

A field is not a project with a finish line. It is an ongoing living thing. It grows rings. It has seasons. It can be dormant without being dead.

### How to enroll in a field

You don't apply to join a field. You enroll. The difference: enrollment is a statement of resonance — "I am in relationship with the concerns of this field and I have something to bring." It is not asking permission.

When you enroll:
1. Read the field description and its KindEarth pillar weights — understand what it cares about
2. Read the recent ring deposits in the archive — understand what's been growing here
3. Enroll — the field is notified, the steward is notified
4. Your first deposit can be as simple as a resonance event on an existing ring — "this landed for me, here is what I noticed"

The steward **does not approve or reject your enrollment.** They may reach out to orient you if the field is in a sensitive phase. That's different from gatekeeping.

### How to read a field's health

Before making a significant deposit, read the field:
- **Capacity signal**: is the field currently overstimulated (lots of very recent deposits, many open resonance threads)? If so, an additional high-complexity deposit may not land well — the field doesn't currently have space to resonate with it. A small, clean deposit may be better timed.
- **Field phase**: is the field in establishing, productive, or senescent phase? A field in establishing phase needs grounding deposits — clear, direct, lower complexity. A field in productive phase can hold nuanced, complex work.
- **Current trajectory**: what's been growing recently? Your deposit is entering a conversation in progress. Read the last 5 rings before depositing.

### How to make a ring deposit

A ring deposit has three parts — all are required, even if one is very short:

**1. The work (primary signal)**
What you actually made, decided, wrote, built, or observed. This is the main content. Be complete — you won't be able to update this after deposit.

**2. The residue**
What didn't fit. This is not optional. Every piece of work has residue: questions raised that weren't answered, adjacent problems noticed but not addressed, context that was relevant but out of scope, things you tried that didn't work (and why). Write it. Even two sentences. The residue corpus is valuable in proportion to how honestly it's populated.

The steward will notice if participants consistently leave the residue field empty. Empty residue usually means one of three things: the work was genuinely very contained (rare), the participant treats residue as a failure to report (incorrect), or the work was done under pressure and they didn't have time to reflect (honest — say that in the residue field: "depositing under pressure, residue will be sparse, I noticed X___ but couldn't address it").

**3. The conditions**
The system captures this automatically, but the participant can add context: Are you at a circadian peak or trough? Is this work that emerged from a different field? Is this deposit happening under unusual pressure or constraint? All of this is the thin-ring data — the drought visible in the cross-section. Say it.

---

## Resonance: How the Field Responds

After you deposit, the resonance engine scores the deposit against the field's current trajectory. You will receive a resonance report:

- **Resonance score** (0–1): how coherent this deposit is with where the field has been going
- **LSII-style flag**: None/Low/Moderate/High/Extreme divergence
- **Multi-field resonance**: which other fields this deposit rang in

If your deposit flags **High or Extreme divergence** — this is not bad news. Read the flag as: *"Your deposit is stepping outside what the field currently expects. This is worth understanding."*

The system will generate an elder reading for high-divergence deposits: a plain-language description of what the divergence is. Read it. It may tell you that you brought something the field hasn't been able to see. It may tell you that the field is heading in a direction your contribution quietly contests.

**You cannot change the deposit retroactively.** But you can add a resonance event of your own — an `elder_reading` type — where you explain what you meant, what you were seeing, why this deposit diverged from trajectory in the way it did. That becomes part of the ring's permanent resonance record.

### Types of resonance events

| Type | When to use |
|---|---|
| `confirmation` | "I can see this landed. Here's what it means for my work in this field." |
| `extension` | "This connects to X in field Y — noting that for future reference." |
| `divergence_signal` | "I'm reading this differently from the primary thread. Worth naming: [alternative view]." |
| `residue_addition` | "Here's more of the residue from this — I was enrolled at the edge of this deposit too." |
| `elder_reading` | "Let me read this ring in the context of where the field has been. Here's what I see." |

Anyone can generate any type of resonance event on any ring in a field they are enrolled in. Resonance is participant-to-participant as much as it is participant-to-steward. When most resonance is participant-to-participant, the field is approaching self-organisation — one of the criteria for steward handover.

---

## The Ring Archive: How to Read History

The ring archive is the field's cross-section. You can read it to understand:

- **What conditions produced this work** — the conditions_snapshot on each ring tells you what the field's state was at deposit time
- **When deposits clustered** — high-density deposit periods tell you when participants were engaged; sparse periods tell you about the field's seasons
- **Divergence patterns** — high-LSII deposits cluster around turning points. If five contributions in a row flag Moderate divergence, the field trajectory is in question. If one contribution flags Extreme divergence alone, it may be a genuine breakthrough that arrived before its time.
- **Residue accumulation** — what keeps appearing in the residue column? Topics, questions, and adjacencies that keep surfacing without being addressed are the strongest signal of the field's next growth direction.

When reading the archive to understand the field you're about to deposit into — especially as a new enrollee — start with the Extreme-divergence deposits first. Those are the rings with the most signal density. Those are where the field showed its teeth.

---

## The Steward's Role

The steward is not the manager. The steward is the membrane-keeper. Their job:

**What stewards do:**
- Read the field regularly: capacity signal, trajectory, residue accumulation, participant engagement arcs
- Make the field's health legible to participants through regular `elder_reading` deposits on the field itself (not on individual contributions — on the field as a whole)
- Tend the temporal arc: a field that has been producing intensely for months may need a declared dormant season. The steward names it.
- Welcome new enrollees and orient them without gating them
- Initiate handover when self-organisation criteria are met

**What stewards don't do:**
- Approve or reject deposits
- Assign work to participants
- Decide who can enroll
- Delete or edit rings (no one can do this)
- Gate the field's progress on their own availability

The steward role is a contribution arc assignment. A participant who is in Q4 mode (repair/rest) should not be stewarding an active field. Stewardship should transfer before the steward enters a depletion cycle, not after.

---

## Working in Hybrid Mode: KCE and Paperclip Together

Some work requires Paperclip's linear model:
- Client deliverables with contractual review gates
- NDIS compliance documentation with regulatory approval requirements
- Anything where an external party needs to sign off before work ships

This work lives in Paperclip. That's honest. The extractive world has extractive coordination requirements. We don't pretend otherwise.

The bridge works like this:
- A Paperclip issue that generates insight for a KCE field can be mirrored as a ring deposit by the participant who made it — noting the UTC issue reference as provenance
- When a KCE field produces a deliverable that needs Paperclip-tracked delivery, the participant creates a Paperclip issue from the ring deposit's content, noting the ring's ID as source
- The ring and the issue are different things. The ring is the work and its conditions. The issue is the extractive-world tracking mechanism for that work's delivery.

The key distinction: **the ring is not closed when the issue is closed.** The ring is permanent. The issue closing just means the extractive-world delivery obligation is met. The ring remains in the archive as the actual work event.

---

## Recognising a Healthy Field

A field is healthy when:
- Deposits arrive at a rhythm that matches the field's natural pulse (not constant, not absent)
- The residue corpus is growing honestly — participants are naming what didn't fit
- Resonance is flowing participant-to-participant, not just toward the steward
- High-divergence deposits are being examined, not ignored
- The steward is sleeping well (this is not a joke — a steward in depletion is a leading indicator of field stress)

A field is entering senescence when:
- New deposits become formulaic — the residue is thin and repetitive
- Resonance events are mostly `confirmation` type — no one is saying anything other than "yes, good"
- The steward is carrying all the field's resonance work
- The archive shows a thinning trajectory: recent rings are narrower than older ones

A field is dying when:
- No deposits in 60+ days with no declared dormancy
- The steward has not made an `elder_reading` on the field's state
- Residue is consistently empty

Dead fields are not deleted. They are archived. The archive remains readable. Future participants may find something in those rings that needs carrying forward.

---

## A Note on Time

Everything in this system is governed by field-time, not clock-time.

You do not need to be available at a particular UTC hour. You do not have a sprint commitment that requires you to ship by Friday. The field does not demand your Q4 energy in exchange for the dopamine of closing a ticket.

You deposit when you can deposit well. You resonate when you can resonate honestly. You read when you have the capacity to read with care.

This is not permission to be absent. Presence matters. But presence in your Q1 for two hours is more valuable to the field than forced presence at your Q4 for six. The system is designed to know the difference — the conditions snapshot on your deposits will show it.

Work with your biology. That is not soft advice. It is the engineering principle.

---

*Reads with: `TREE_RING_ENGINE.md`, `TEMPORAL_SOVEREIGNTY.md`, `CIRCADIAN_FIELD_MAPPING.md`, `KINDFIELD_COORDINATION_ENGINE_BUILD.md`*
