# The Tree-Ring Engine
### Architecture of the KindField Coordination Engine — Immutable, Conditions-Preserving, Resonant

*Version 1.0 — March 2026*

---

## The Metaphor, Made Precise

A tree ring is:

1. **Immutable** — the ring from 1987 cannot be revised. The drought is in the ring. The good years are in the ring. The fire year is in the ring. No re-review, no post-hoc correction, no overwriting.

2. **Conditions-preserving** — the width of the ring encodes the conditions at the time of growth. A thin ring in 1976 is not a failure to grow. It is accurate data: this was a stress year. Future readers can see it, use it, understand what was happening that year. The conditions are preserved in the ring itself.

3. **Temporally faithful** — rings are in sequence. The tree cannot lie about what came before what. The structure is the history.

4. **Multi-contextually readable** — a ring in a Douglas fir in Oregon is in dialogue with rings in Chilean araucarias and Siberian larches from the same year. The same volcanic event shows across all of them. One tree, one ring, but the event it records is readable across a global corpus. The data is not siloed to the tree that recorded it.

5. **Additive, not replacive** — each new ring adds to the tree's structural integrity without replacing what came before. Growth is accumulation, not revision.

The conventional PM system (Paperclip, Linear, Jira, GitHub Issues) violates every one of these principles. Issues are closed, edges are lost, revisions overwrite context, work is re-opened and re-scoped, history is technically browsable but epistemically discarded. The merge commit replaces the branch. The approved ticket replaces the discussion. The shipped feature replaces the question that motivated it.

The Tree-Ring Engine implements coordination that respects all five properties.

---

## The Entity Model

### Fields (not Companies or Projects)

A **Field** is a relational zone with its own KindEarth governance parameters, resonance sensitivity, and temporal arc. Fields are not containers for work. They are living structures that grow through ring deposits.

A field has:
- A **steward** — not a manager. A membrane-keeper who reads field health and maintains the conditions for contribution. The steward does not approve or reject contributions; they tend the field's resonance environment.
- **KindEarth pillar weights** — each of the five gates applies with different weighting in different fields. A care field weights Relational Accountability most heavily. A technical field may weight Practical Stewardship more. The weights are explicit.
- **Field constants** — the k values in Φ=km^n for different contribution types in this field. Sets the sensitivity of the field to different kinds of deposits.
- **Temporal arc** — the field's current season/phase. A newly established field is in a different temporal arc than a mature field whose BEC threshold is approaching.
- **Capacity signal** — not a budget. A reading of the field's current relational carrying capacity: how much contribution can land meaningfully right now? A field that is overstimulated has low capacity. A field that is dormant has different needs from a field at peak productive phase.

Fields **do not expire.** A field can be dormant. A field can archive. A field is never deleted — its rings are permanent. The steward may change. The participants may change. The field persists.

### Ring Deposits (not Issues or Tickets)

A **Ring Deposit** (or Contribution) is an atomic, immutable work event. Once deposited, it cannot be edited, deleted, or re-opened. It is the ring. The conditions at the time of deposit are preserved in the deposit itself.

A ring deposit contains:
- **content** — the work product: code, text, decision, analysis, care event, field observation
- **residue** — what didn't fit the task frame: the edge cases that weren't in scope, the adjacent problems that surfaced, the questions raised but not answered, the context that was too wide for the contribution itself. This is first-class data, not a footnote.
- **conditions_snapshot** — the state of the field at deposit time: field phase, active participants, recent resonance signals, capacity signal, temporal arc position
- **temporal_context** — field-time coordinates (see `TEMPORAL_SOVEREIGNTY.md`)
- **multi_field_resonances** — the ring's resonance score in every field sensitive to this contribution, not just the primary field. One ring, multiple trees.

What a ring deposit does **not** contain:
- A status (it has no status — it is complete by definition at deposit)
- An assignee (it was made by a participant — it doesn't need to be routed to one)
- A due date (field-time governs when — the ring is deposited when it can be, not by deadline)
- A priority (resonance score determines field weight, not manually assigned priority)

### Participants (not Agents or Users)

A **Participant** is a field-aware contributor with a temporal signature and field sensitivity profile. Participants are not workers assigned to tasks. They are organisms with their own circadian state, field affinities, and contribution arc.

A participant profile holds:
- **temporal_signature** — circadian chronotype (early/neutral/late riser), typical peak ultradian phase duration, current season context
- **field_sensitivities** — which fields this participant resonates with strongly, and how (some participants are high-clarity depositors in technical fields; the same participant may be a resonant responder in relational fields rather than a depositor)
- **contribution_arc** — not a skills list. The participant's current trajectory: are they building depth in a domain (Q2 consolidation mode), ranging broadly (Q3 breadth mode), or in a rest/repair cycle (Q4 mode)?
- **residue_affinity** — some participants are naturally good at naming what didn't fit. Their residue deposits are often more valuable than their primary contributions.

Participants **self-select into fields** through enrollment. They are not assigned. The steward does not approve enrollment (though they may be consulted); the field's resonance with the participant is what matters. A participant who cannot resonate with a field will not contribute meaningfully — the system can indicate this gently without gatekeeping.

### Resonance Events (not Comments or Reviews)

A **Resonance Event** is a response to a ring deposit. It is not a comment (which implies the ring can be changed). It is not a review (which implies a gate to pass through). It is a signal that attaches to the ring permanently, as part of the ring's resonance record.

Resonance events are:
- **Immutable** — once made, they are part of the ring's record. You can add more resonance events. You cannot un-resonate.
- **Non-blocking** — resonance events never gate future work. They inform. They enrich. They do not stop.
- **Typed** — each resonance event has a type: `confirmation` (this landed, I can see it), `extension` (this connects to X in another field), `divergence_signal` (I'm reading this differently — worth noting), `residue_addition` (here's more of what didn't fit), `elder_reading` (interpretation of the ring's significance in the field arc)

A high-divergence resonance event — one that disagrees strongly with a deposit — is the most valuable type. It is not rejection. It is signal. The system should make this explicit: **divergence is not rejection. It is the most informative resonance.**

This is the direct structural opposition to the review/approve model where divergence = the thing didn't pass. In the tree-ring model, divergence = the ring is showing us something the field needs to understand.

---

## The LSII Resonance Score

Every ring deposit is scored by the resonance engine after deposit. The score is not computed before or during — it cannot change the deposit. It is a property of the ring observed in retrospect.

The resonance score is computed as a variant of the LSII (from `kindpath-analyser`):

**How much does this contribution diverge from the field's current trajectory?**

```
resonance_score = 1.0 - lsii_equivalent_divergence
```

High resonance_score = deposit is coherent with field trajectory.
Low resonance_score = deposit diverges significantly from field trajectory.

**Important:** neither is better. They are different.

- High resonance: contributes to continuity. Field is deepening in its current direction.
- Low resonance (high divergence): the deposit is stepping outside the field's frame. This may be:
  - A creative breakthrough (the field hasn't been able to see this)
  - A signal that the field itself needs to shift direction
  - A participant bringing material from a different field that this one needs
  - The equivalent of a high-LSII song: something changed. Worth examining.

The LSII flag levels apply directly:

| Flag | Score range | Meaning for contributions |
|---|---|---|
| None | 0.8–1.0 | Deep resonance with field trajectory |
| Low | 0.6–0.8 | Slight divergence — generative friction |
| Moderate | 0.4–0.6 | Notable shift — flag for field attention |
| High | 0.2–0.4 | Significant divergence — may indicate field trajectory needs review |
| Extreme | 0.0–0.2 | The participant is bringing something the field can't currently hold — most valuable type |

Extreme-flagged contributions receive an automatic `elder_reading` from the resonance engine: a plain-language description of what the divergence is and what it might mean for the field.

---

## Multi-Contextural Ring Resonance

The tree-ring metaphor's most important property: a ring is not private to one tree. The same volcanic event (Tambora, 1815) shows in rings across the Northern Hemisphere. The information is not confined to the tree that recorded it.

In the KCE, a single ring deposit can resonate across multiple fields simultaneously.

The mechanism:
1. Deposit is made to a **primary field** — the field the participant is enrolled in that is most directly relevant.
2. The resonance engine computes the deposit's feature vector: topic, domain, skill type, relational content, residue content.
3. The feature vector is matched against the **sensitivity profiles** of all active fields.
4. Fields that are sensitive to this content type receive a **resonance signal** — not the contribution itself (that belongs to its field), but the signal that this content exists and is available for reference.
5. The deposit's `multi_field_resonances` array records all fields it resonated in, with their individual scores.

Practically: a contribution about NDIS boundary conditions in one field might resonate in the care field, the data-capture field, and the legal-compliance field simultaneously. The care field doesn't get assigned the work. It gets the signal that this content exists, and participants in that field who are sensitive to it can draw on it.

This replaces the explicit cross-team notification / @mention / duplicate-issue pattern with a **sensitivity-based resonance network**. The routing is relational, not administrative.

---

## The Ring Archive

The Ring Archive is the permanent, append-only ledger of all deposits. It is the structural record — the cross-section of the tree. Every ring in sequence, with its conditions snapshot preserved.

The Ring Archive is:
- **Queryable** — you can retrieve rings by field, by participant, by temporal arc, by resonance score, by residue type, by multi-field resonance
- **Never editable** — the only operation is append. No ring is ever deleted or modified.
- **Conditions-legible** — querying the archive with conditions context enabled shows not just what was deposited but what the field and participant state was when it was deposited.
- **Temporally indexed** in both UTC (forgazi bridge) and field-time (primary coordinate)

The archive is not a blame record. It is not an audit log in the compliance sense. It is the tree's cross-section — read to understand what conditions produced each layer of growth, not to assign accountability for thin rings.

---

## Self-Dismantling Criteria

The five gates in `AGENTS.md` include Reflective Continuity and Practical Stewardship. Applied to fields:

A field should be evaluated for archiving or handover when:

1. **Self-organisation rate** > 70%: participants are structuring their own contribution patterns without steward intervention
2. **User-generated resonance** > 60%: most resonance events are participant-to-participant, not participant-to-steward
3. **Intergenerational pattern**: new participants are learning from the ring archive, not from the steward
4. **Field can read itself**: the accumulated ring archive contains sufficient density to answer questions about field health without external analysis tools

When these are met, the steward initiates handover protocol:
- Document the field's trajectory in a final `elder_reading` ring deposit
- Transfer stewardship to the most field-resonant active participant
- Archive the steward's own participant role (they become a dormant member — still readable in the ring archive, no longer active)
- The field continues without them

This is the structural implementation of the KindEarth principle: **design for your own obsolescence.** A field that needs its steward to function is a field that hasn't grown rings yet. A field that can function without its steward is a field that has.

---

## What This Engine Replaces, and What It Doesn't

### Replaces
- The **issue/ticket model** (linear, ephemeral, status-gated)
- The **review/approve gate** (divergence-as-rejection)
- The **sprint/deadline model** (clock-time primacy over biological reality)
- The **assigned-work model** (top-down routing over relational self-selection)
- The **completion-and-discard pattern** (work history treated as operational overhead)

### Does Not Replace
- **Paperclip** for client-facing, compliance-required, or extractive-world-adjacent work — that requires the linear model because the extractive world operates on it. The bridge is explicit.
- **GitHub** for code versioning — code repositories have their own ring model (git history is already immutable and append-only). The KCE doesn't duplicate what git does.
- **Documentation** - the archive is not a wiki. The rings are contributions; documentation is a specific kind of contribution that gets deposited like any other.
- **Decision-making** for high-stakes irreversible choices — those warrant deliberate process, not relational resonance alone.

---

## The Philosophical Commitment

The tree-ring engine is an epistemological commitment before it is a software architecture.

The commitment: **the conditions that shaped a contribution are as important as the contribution itself, and must be preserved alongside it.**

A piece of code written under time pressure, by an overextended participant, during a field capacity crisis, during a Q4 late-night session, in a thin ring year — is not the same as the same code written in unhurried depth by a participant at peak capacity. The external output may be identical. The conditions that produced it are not. Those conditions are data.

The tree doesn't hide the drought. The ring doesn't pretend all years are equal. The archive doesn't lie about what was happening when each layer was laid down.

That is the engine.

---

*Reads with: `WHOLE_DATA_ACCOUNTING.md`, `TEMPORAL_SOVEREIGNTY.md`, `KINDFIELD_COORDINATION_ENGINE_BUILD.md`, `THE_FIELD_EQUATION.md`*
