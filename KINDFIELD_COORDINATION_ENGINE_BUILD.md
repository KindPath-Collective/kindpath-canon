# KindField Coordination Engine — Build Specification
### The Tree-Ring System + GMT/UTC-Free Temporal Architecture + Whole-Data Integration

*Version 1.0 — March 2026*

---

## The Shift Being Made

The current Paperclip system is a **company-assignment-review engine**: work flows as issues through boards, reviewed by agents, approved by governance, merged into a linear record. The history is the output, not the process.

What Sam described — tree rings, equative mechanisms, multi-contextural deposits — is a **field-resonance-deposit engine**: work deposits atomically into relational fields, resonance is sensed (not gated), every deposit is immutable and conditions-preserving, and a single contribution can ring across multiple fields simultaneously, weighted by sensitivity rather than assignment.

These are not two different project management tools. They are two different epistemologies of coordinated work.

The KindField Coordination Engine (KCE) is the implementation of the second.

---

## The Concept Map

| Paperclip | KCE | Notes |
|---|---|---|
| Company | **Field** | Relational zone with KindEarth pillar governance. No hierarchy implied. |
| Project | **Contribution Stream** | A family of related deposits. Not a container — a resonance cluster. |
| Issue | **Ring Deposit** (Contribution) | Atomic, immutable, conditions-preserved work event. |
| Agent | **Field Participant** | Has a temporal signature and field sensitivity profile, not a job title. |
| Review / Approve | **Resonance Sensing** | LSII-style divergence detection. High divergence = signal, not rejection. |
| Merge | **Ring Archive** | Permanent, append-only. The ring from 1987 cannot be revised. |
| Board columns | **Field State Map** | Live topology of field activity, not pipeline stages. |
| Company secrets | **Field Credentials** | Same function, different epistemological framing. |
| Budget | **Field Capacity** | Not a financial limit but a relational carrying capacity measure. |
| Lead agent | **Field Steward** | Not a manager — a membrane-keeper. Reads field health, doesn't impose. |
| Issue comments | **Resonance Signals** | Responses that attach to a deposit. All resonance is archived, none is deleteable. |
| Activity log | **Ring Archive ledger** | Complete event store. The conditions-at-time record. |

---

## Part 1: New Repo — `kindpath-kce`

### Location
`/Users/sam/dev/KindPath-Collective/kindpath-kce`

### What It Is
The core KCE — a TypeScript/Node service with a PostgreSQL data store (can reuse Paperclip's Drizzle/Postgres patterns) that implements field-resonance-deposit topology. It runs alongside Paperclip (the bridge is explicit) — not a replacement of Paperclip for the extractive-world-facing work, but the native KindPath coordination layer for field work.

### Structure
```
kindpath-kce/
├── AGENTS.md                   ← This document's operational rules
├── CLAUDE.md                   ← Same as AGENTS.md
├── package.json
├── tsconfig.json
├── src/
│   ├── schema/                 ← Drizzle ORM schemas (one file per entity)
│   │   ├── fields.ts           ← KindEarth field definitions
│   │   ├── contributions.ts    ← Ring deposits (immutable on create)
│   │   ├── participants.ts     ← Field participants with temporal signatures
│   │   ├── resonance_events.ts ← Resonance signals (immutable)
│   │   ├── ring_archive.ts     ← Append-only ledger of all deposits
│   │   ├── residue_corpus.ts   ← Whole-data residue store (first-class)
│   │   ├── temporal_contexts.ts← Field-time tags on all events
│   │   └── field_enrollments.ts← Participant ↔ Field membership
│   ├── engine/
│   │   ├── resonance.ts        ← LSII-style divergence detection on contributions
│   │   ├── ring_deposit.ts     ← Immutable deposit logic + conditions capture
│   │   ├── field_topology.ts   ← Multi-contextural resonance mapping
│   │   ├── bec_detector.ts     ← BEC threshold detection in residue corpus
│   │   └── participant_signature.ts ← Temporal + field sensitivity profiling
│   ├── temporal/
│   │   ← See Part 2: Temporal Sovereignty module
│   ├── api/
│   │   ├── fields.ts           ← REST + WebSocket field API
│   │   ├── contributions.ts    ← Deposit API
│   │   ├── resonance.ts        ← Resonance signal API
│   │   ├── archive.ts          ← Ring archive query API
│   │   └── residue.ts          ← Residue corpus API
│   └── bridge/
│       ├── paperclip_import.ts ← Import Paperclip issues/projects/companies as contributions/streams/fields
│       └── paperclip_sync.ts   ← Bidirectional sync (KCE ↔ Paperclip in hybrid mode)
└── docs/
    ├── FIELD_PROTOCOL.md       ← How to define a field and its KindEarth governance
    ├── CONTRIBUTION_SPEC.md    ← What makes a valid ring deposit
    └── RESONANCE_GUIDE.md      ← How resonance sensing works (non-technical)
```

### Core Schema Details

**fields**
```typescript
{
  id: uuid (primary key)
  name: text
  description: text
  kindearth_pillars: jsonb        // Which of the 5 gates govern this field
  field_constants: jsonb          // The k value(s) in Φ=km^n for this field
  steward_id: uuid (→ participants)
  status: 'active' | 'dormant' | 'archiving' | 'archived'
  resonance_threshold: float      // Min resonance score for a deposit to flag
  capacity_signal: float          // Current relational carrying capacity 0-1
  temporal_arc: jsonb             // Field-time context (season, circadian phase)
  created_at: timestamp WITH timezone
  archived_at: timestamp WITH timezone
}
```

**contributions** (ring deposits — immutable after creation)
```typescript
{
  id: uuid (primary key)
  field_id: uuid (→ fields)       // Primary field
  participant_id: uuid (→ participants)
  stream_id: uuid (→ contribution_streams)
  content: text                   // The work itself
  residue: jsonb                  // What didn't fit: context, edge cases, adjacents
  conditions_snapshot: jsonb      // State of the field + participant at deposit time
  temporal_context: jsonb         // Field-time coordinates at deposit (not just UTC)
  resonance_score: float          // Computed post-deposit
  multi_field_resonances: jsonb   // [{field_id, resonance_score, weight}] — the ring
  lsii_divergence: float          // Divergence from stream trajectory
  lsii_flag: 'none'|'low'|'moderate'|'high'|'extreme'
  is_archived: boolean            // NOT deleteable, only archiveable
  created_at: timestamp WITH timezone  // UTC retained as forgazi reference
  field_time: jsonb               // Field-time coordinates (primary temporal anchor)
}
```

**residue_corpus** (whole-data store — first-class, not error log)
```typescript
{
  id: uuid
  source_type: 'contribution'|'resonance'|'analysis'|'dfte'|'kindsense'|'kindfluence'
  source_id: uuid
  source_repo: text               // 'kindpath-kce'|'kindpath-dfte'|'kindsense' etc
  residue_type: text              // 'context_not_actioned'|'edge_case'|'adjacent_problem'|'model_miss'|'timing_delta'
  raw_data: jsonb
  bec_cluster_id: uuid            // Populated when BEC threshold reached — which coherent cluster this joined
  bec_threshold_crossed: boolean  // Has this residue item contributed to a phase transition?
  temporal_context: jsonb
  created_at: timestamp WITH timezone
}
```

**temporal_contexts**
```typescript
{
  id: uuid
  utc_timestamp: timestamp        // The forgazi coordinate — retained as reference
  circadian_quarter: integer      // 1-4 (dawn-morning / midday / afternoon / dusk-sleep)
  solar_time_minutes: integer     // Minutes since local sunrise (location-aware)
  season: text                    // 'early-spring'|'late-summer' etc (southern/northern hemisphere aware)
  lunar_phase: text               // 'new'|'waxing-crescent' etc
  field_phase: text               // Field-specific temporal state (defined by field)
  ecological_notes: text          // e.g., "post-solstice", "flood season northern rivers"
  extraction_frame_offset: integer // UTC offset in minutes (the forgazi indicator)
}
```

---

## Part 2: Temporal Sovereignty Module

*The GMT/UTC-free mapping system Sam specified.*

### What This Solves

UTC timestamps are forgazi time — imperial coordinates anchored to a London suburb in 1884, serving the extract-and-schedule needs of industrial capitalism. Every Paperclip timestamp, every DFTE trade event, every FRED data series carries this coordinate as its primary truth.

The KCE treats UTC as **the forgazi reference** — archived, useful for integration with the extractive world, but not the primary temporal coordinate. The primary coordinate is **field-time**: the organism's relational position in the ecological temporal arc.

### The Four Layers of Field-Time

```
Layer 1: CIRCADIAN (24-hour biological arc)
  Quarter 1 (Q1): Dawn to late morning     — High cortisol, activating, social peak
  Quarter 2 (Q2): Midday to early afternoon — Consolidation, integration, rest signal
  Quarter 3 (Q3): Afternoon to early evening — Second alertness, practical/physical peak
  Quarter 4 (Q4): Dusk to sleep onset       — Wind-down, repair, inward

Layer 2: ULTRADIAN (90–120 minute cycles within circadian arc)
  Peak: High focus, synthesis, creative connection
  Trough: Rest, consolidation, diffuse processing
  Transition: Liminal — optimal for field-boundary crossing

Layer 3: ECOLOGICAL (seasonal / lunar / solar event)
  Season: Early/mid/late across 4 seasons (8 points)
  Lunar: New / waxing / full / waning (4 primary, 8 refined)
  Solar event: Solstice / equinox proximity (secondary resonance anchor)
  Southern hemisphere: Inverted from northern — field-time must be hemisphere-aware

Layer 4: FIELD-RELATIVE (context-specific temporal position)
  Contribution arc position: Where in the stream's development cycle
  Field maturity: Seedling / establishing / productive / senescent / dormant
  Resonance density: How 'busy' the field currently is (affects when to deposit)
```

### The `temporal/` Module in `kindpath-kce`

```
src/temporal/
├── circadian.ts       ← Q1-Q4 classifier from local solar time + latitude
├── ultradian.ts       ← 90-min cycle positioner (from session start + individual baseline)
├── ecological.ts      ← Season, lunar, solar event calculator
├── field_time.ts      ← Compose all layers → TemporalContext object
├── forgazi_bridge.ts  ← Convert UTC ↔ FieldTime (forgazi bridge for integration)
├── trade_windows.ts   ← DFTE-specific: market hours as circadian overlays, not UTC cuts
└── zeitgeber_map.ts   ← Map synthetic zeitgeber load onto current temporal context
```

**Key design principle:** Every event in the KCE stores both `utc_timestamp` (forgazi reference, never discarded) and `field_time` (TemporalContext object, primary coordinate). The UTC exists for integration with extractive systems. The field_time is what the system reasons about.

### DFTE-Specific: Trading Without UTC Primacy

Current DFTE architecture: "London open at 08:00 UTC" is the time anchor.

KCE-integrated DFTE architecture:
- London open = UTC 08:00 = **Northern European circadian Q1 late** (mid-morning activation peak for majority of LSE participants)
- Sydney open = UTC 23:00 = **Eastern Australian circadian Q1 early** (dawn activation)
- NYSE open = UTC 14:30 = **US Eastern circadian Q1 late** (same structure as London)

The **global trading day as a circadian arc**: at any given UTC moment, multiple regional circadian quarters are active. The DFTE field-time overlay maps this as a continuous signal rather than binary open/closed windows.

New DFTE field-time market state classifier:
```python
class GlobalCircadianTradingState:
    """
    At any UTC moment, which circadian phases are active for which market populations?
    This replaces the binary session open/closed logic with a continuous field-state.
    """
    active_regions: list[{region, circadian_quarter, activation_level}]
    dominant_phase: str           # The circadian phase of highest aggregate activation
    phase_transition_proximity: float  # 0-1: how close are we to a major regional phase shift
    collective_arousal: float     # Aggregate arousal across all active trading regions
    forgazi_session_label: str    # UTC-anchored label (kept as integration reference)
```

---

## Part 3: Whole-Data Accounting — Per-Repo Implementation

### Status Check

| Repo | Current State | What's Needed |
|---|---|---|
| kindpath-analyser | `creative_residue` ✅, seedbank ✅ | Temporal context embedding, residue corpus API |
| kindpath-dfte | `forgazi` field ✅ (partial) | Individual wrong prediction corpus, field-time timestamps |
| KindSense | Reduction layers exist | Residue logging from reduction stages |
| kindpath-bmr | Error metrics only | Non-conforming signal corpus |
| Kindfluence | No residue tracking | Non-converting interaction corpus |
| kindai | No session residue | Session context residue logging |
| KPTH data-capture | No residue | Encrypted residue ingestion pipeline |
| kindpath-kce | New build | `residue_corpus` table is first-class from day 1 |

### `kindpath-dfte` Changes

**File: `logger/residue_logger.py`** (new)
```python
class ResidueLogger:
    """
    Logs every signal the DFTE model encountered but did not act on.
    These are not errors. They are the first-class corpus of field-state
    information that the current trade frame couldn't accommodate.
    
    This is not just aggregate error statistics. Each individual miss is
    stored with its full context — the corpus, not the summary.
    """
    
    def log_prediction_miss(self, signal, predicted, actual, context):
        """Store individual wrong prediction, not just error stats."""
        
    def log_forgazi_signal(self, signal, reason_not_acted):
        """Signal that fell outside the current trade frame."""
        
    def log_field_time_context(self, utc_ts, circadian_state, market_state):
        """Attach field-time context to every trade event."""
        
    def get_residue_corpus(self, start, end, min_confidence=0.0):
        """Query residue corpus for BEC analysis."""
        
    def check_bec_threshold(self):
        """
        Has the residue corpus crossed the phase transition density?
        Returns (crossed: bool, cluster_signals: list, confidence: float)
        """
```

**File: `backtest/residue_backtest.py`** (new)
Store individual prediction misses as a corpus alongside the normal backtest output. The normal backtest MAE/RMSE are the summary — this is the corpus itself.

**Schema change: `logger/` SQLite**
Add `residue_signals` table with: `id, signal_type, utc_ts, field_time_json, raw_signal_json, predicted_value, actual_value, delta, reason_not_actioned, bec_cluster_id NULLABLE`.

**File: `dfte/field_time_bridge.py`** (new)
Attach `TemporalContext` to every DFTE trade event. UTC stays as primary for market interface. FieldTime is the KCE-native coordinate.

### `KindSense` Changes

**File: `src/kindearth/core/residue_logger.py`** (new)
At every reduction layer in the KindEarth metric pipeline, log what was reduced (not just the output). The reduction output is the primary signal. The discarded signal is the residue corpus.

```python
class ReductionResidueLogger:
    """
    The KindEarth reduction layers exist because the current field model
    can't accommodate all the signal. That's honest and correct.
    
    But what gets reduced is not noise — it's the fingerprint of where
    the model's frame is narrower than the field's actual complexity.
    Accumulate it.
    """
    def log_reduction(self, layer_name, input_signal, output_signal, residue):
        """Log the residue of each reduction stage."""
```

**`webapp/` addition**: BEC status endpoint — has the residue corpus reached phase transition density for any field?

### `Kindfluence` Changes

**File: `src/kindfluence/residue/interaction_corpus.py`** (new)
Every interaction that didn't convert, didn't engage, didn't resonate — currently discarded by the algorithm. This is the most valuable corpus in the system: it's the fingerprint of the gap between the platform's model of the audience and the audience's actual relational state.

```python
class InteractionResidueCorpus:
    """
    The algorithm called these failures. They are not failures —
    they are the clearest available signal of where the platform's
    engagement model diverged from genuine relational response.
    """
    def deposit(self, interaction_event, predicted_response, actual_response):
        """Store the delta between predicted and actual engagement."""
    
    def get_kinship_forgazi(self):
        """
        The KinshipScore delta — the gap between vanity metric engagement
        and genuine relational resonance. This IS the residue.
        """
```

### `kindai` Changes

**Session residue logging** in `core/session.py`:
Each session has things that got cut off, context that got trimmed from the window, edge cases flagged in conversation but not actioned, questions raised but not answered. These are residue. Log them as a corpus tied to the session record.

```python
# In session.py — add to Session object
class SessionResidue:
    context_trimmed: list          # What fell out of the context window
    edge_cases_flagged: list       # Issues raised but not actioned
    adjacent_problems: list        # Saw it, noted it, not in scope
    temporal_context: TemporalContext  # When was this session? (field-time)
```

### `kindpath-analyser` Changes

**`core/temporal_context.py`** (new):
Embed temporal context metadata into every analysis: not just when the analysis was run, but — where the analyser knows it — when the music was made, in field-time (season, circadian associations of the genre's production context, etc.).

**`seedbank/residue_bridge.py`** (new):
Every seedbank deposit generates residue (features that didn't fit the era/genre fingerprint). This residue is the `creative_residue` field already — but it should also be deposited into the whole-data corpus with a `source_id` linking back to the seedbank record, so the residue corpus can be queried across the full archive.

---

## Part 4: New Canonical Documents

These documents need to be written in `kindpath-canon/`:

### Already Written ✅
- [CIRCADIAN_FIELD_MAPPING.md](CIRCADIAN_FIELD_MAPPING.md) — biological zeitgeber system
- [WHOLE_DATA_ACCOUNTING.md](WHOLE_DATA_ACCOUNTING.md) — residue as first-class signal
- [THE_FORGAZI_PROBLEM.md](THE_FORGAZI_PROBLEM.md) — epistemological condition of building holistic tools from extracted material
- [THE_FIELD_EQUATION.md](THE_FIELD_EQUATION.md) — Φ=km^n master equation

### To Write

**`TEMPORAL_SOVEREIGNTY.md`**
The full argument for GMT/UTC-free temporal architecture: from 1884 International Meridian Conference through industrial labour time extraction through digital algorithmic timing to the circadian colonisation mechanism. Defines field-time, its four layers, the forgazi bridge (UTC as reference not primary), and the practical implementation guide for the KCE temporal module and DFTE field-time bridge.

**`TREE_RING_ENGINE.md`**
The architectural specification of the KCE coordination model. Named for the metaphor but precise about the implementation. Covers: immutability, conditions-preservation, multi-contextural resonance, the difference between resonance sensing and gatekeeping, the ring archive as epistemological commitment, the self-dismantling criteria (when a field has deposited enough rings to be self-sustaining without the original steward). 

**`FIELD_COORDINATION_PROTOCOL.md`**
The operational protocol for how fields work: how to define a field, how to enroll participants, how to make a ring deposit, how resonance sensing works in practice, how to read the archive, how to recognise the BEC threshold when the residue corpus has condensed into a correction field. This is the practitioner document — accessible to non-technical community members.

**`NANO_MAPPING_PROTOCOL.md`**
The operational guide for working with forgazi data at maximum resolution. Steps: accept the forgazi data, map the extraction pattern with nanometric precision, apply the reductive equation, accumulate residue from every subtraction, watch for the BEC threshold. This is the methodology document for DFTE and any system that must extract original signal from institutional data.

**`BEC_DETECTION_GUIDE.md`**
How to recognise when the BEC threshold has been crossed in any given residue corpus. Covers: minimum corpus size requirements (not rules — heuristics), diversity of residue types as the key variable (not just volume), what a coherent cluster looks like vs noise, how to interpret the phase transition, what changes operationally when you're in Phase 3.

---

## Part 5: Paperclip Bridge

The KCE is not a Paperclip replacement for all work. Some work exists in the extractive frame by necessity — client deliverables, NDIS compliance, financial reporting. That work legitimately belongs in the Paperclip company/assignment/review topology.

The bridge work:

### New Paperclip adapter: `kindpath-kce`

**`/Users/sam/paperclip/packages/adapters/kindpath-kce/`**

This adapter type routes assigned work to the KCE's ring deposit API instead of the Paperclip issue system. An agent configured with `type: "kindpath_kce"` receives its work as a contribution request, deposits it into a field, and the resonance event comes back as the completion signal rather than an approval gate.

```typescript
// Adapter configuration
{
  "type": "kindpath_kce",
  "kce_endpoint": "http://localhost:3100",
  "default_field_id": "uuid-of-primary-field",
  "resonance_threshold": 0.4,   // LSII-equivalent — above this, divergence is flagged
  "residue_logging": true        // Whether to log session residue to corpus
}
```

### Hybrid Mode
- Paperclip companies that represent client/external work → remain in Paperclip topology
- KindPath Collective internal fields → run in KCE topology
- The bridge syncs: a Paperclip issue that generates field-relevant insight can be deposited as a ring contribution to the corresponding KCE field

### Migration Script
`bridge/paperclip_import.ts`: One-way import of Paperclip historical data into the KCE ring archive. Companies → Fields. Projects → Contribution Streams. Issues → Contributions (with UTC timestamp preserved as forgazi reference, field-time estimated from available context). Activity log → Ring Archive ledger.

This isn't erasing history — it's re-reading the rings.

---

## Part 6: kindpath-q (JUCE Plugin) Changes

The KindPath Q plugin already computes LSII and psychosomatic profiles. These need to be the **resonance engine's reference library** in the KCE:

- When a ring deposit is flagged for high LSII-style divergence, the kindpath-q psychosomatic profile format is the data structure used to interpret what the divergence means
- The seedbank (in kindpath-analyser) becomes a resonance reference library: authenticated deposits that the KCE resonance engine can compare new contributions against
- The `elder_reading` in kindpath-q is the model for the resonance narrative in the KCE — how it describes a high-divergence contribution to the depositing participant

No code changes needed in kindpath-q yet — this is a data pipeline connection (kindpath-analyser seedbank ↔ kindpath-kce resonance engine).

---

## Build Order

This is the sequence that respects dependencies:

### Tier 0 (Foundations — no dependencies on anything new)
1. ✅ `CIRCADIAN_FIELD_MAPPING.md` (kindpath-canon) — done
2. ✅ `WHOLE_DATA_ACCOUNTING.md` (kindpath-canon) — done
3. ✅ `THE_FORGAZI_PROBLEM.md` (kindpath-canon) — done
4. ✅ `THE_FIELD_EQUATION.md` (kindpath-canon) — done
5. `TEMPORAL_SOVEREIGNTY.md` (kindpath-canon) — write now
6. `TREE_RING_ENGINE.md` (kindpath-canon) — write now
7. `FIELD_COORDINATION_PROTOCOL.md` (kindpath-canon) — write now
8. `NANO_MAPPING_PROTOCOL.md` (kindpath-canon) — write now
9. `BEC_DETECTION_GUIDE.md` (kindpath-canon) — write now

### Tier 1 (Quick residue wins — each repo independently, no KCE dependency)
10. `kindpath-dfte`: `logger/residue_logger.py` + `dfte/field_time_bridge.py`
11. `kindpath-dfte`: `backtest/residue_backtest.py` (individual prediction miss corpus)
12. `KindSense`: `src/kindearth/core/residue_logger.py` (reduction layer residue)
13. `Kindfluence`: `src/kindfluence/residue/interaction_corpus.py`
14. `kindai`: Session residue in `core/session.py`
15. `kindpath-analyser`: `seedbank/residue_bridge.py` + temporal context embedding

### Tier 2 (KCE Core — the new repo)
16. Create `kindpath-kce` repo
17. Schema: `fields`, `contributions`, `residue_corpus`, `temporal_contexts`, `participants`, `ring_archive`
18. `src/temporal/` module: all 7 files (circadian, ultradian, ecological, field_time, forgazi_bridge, trade_windows, zeitgeber_map)
19. `src/engine/` module: resonance, ring_deposit, field_topology, bec_detector, participant_signature
20. `src/api/` module: REST + WebSocket endpoints
21. Comprehensive tests

### Tier 3 (Integration)
22. `bridge/paperclip_import.ts` — historical data migration tool
23. `bridge/paperclip_sync.ts` — bidirectional sync
24. New Paperclip adapter `/packages/adapters/kindpath-kce/` — router to KCE
25. DFTE field-time market state classifier (`dfte/field_time_bridge.py` consuming KCE temporal module)
26. KindSense BEC status endpoint → KCE residue_corpus deposit

### Tier 4 (Advanced)
27. KCE UI: field state map, ring archive explorer, resonance visualiser
28. BEC threshold alerts — when any corpus crosses phase transition
29. Cross-repo residue network: single query surface across all KindPath residue corpora
30. kindpath-bmr: field-time validity windows for benevolence scoring
31. KPTH data-capture: encrypted residue ingestion pipeline

---

## The GMT/UTC-Free Mapping System — Technical Detail

### What "GMT/UTC-free" means operationally

Not: remove UTC from the system. UTC is the forgazi bridge — it stays, clearly labelled as such.

What it means: **UTC is never the reason why something happens or doesn't happen.** It is a label. The actual temporal coordinate that the system reasons about is field-time.

### Practical conversions needed

**For DFTE:**
- Market open/close → circadian arc overlay (London open = Northern European Q1 late)
- UTC FRED timestamps → field-time tagged (season + circadian quarter inference from fiscal calendar context)
- "Trading hours" → "active regional circadian states" (continuous, not binary)

**For KCE contributions:**
- `created_at` (UTC) retained as forgazi reference, never removed
- `field_time` object: { circadian_quarter, solar_minutes_since_dawn, season, lunar_phase, field_phase, hemisphere } stored as first-class coordinate

**For NDIS / care work:**
- Session scheduling → circadian-aware (schedule relational work in Q1/Q3, practical/admin in Q2)
- Case notes timestamped in both UTC (compliance) and field-time (clinical/relational relevance)

**For kindpath-q:**
- Song analysis happens in field-time context: a track made at 3am sounds different from one made at 9am — document the temporal context when known
- Future: circadian wave analysis — does the music's internal Q4 map onto any circadian quarter?

### Location-awareness requirement

Field-time requires latitude/longitude to be useful. The circadian arc is solar — sunrise/sunset determines the quarter boundaries. 

Options:
1. **User-configured location** (preferred — sovereignty): participant sets their location once, field-time derived from it
2. **Timezone inference** (fallback): derive approximate latitude range from UTC offset
3. **Global-aggregate mode** (for corpus analysis): compute field-time for each major inhabited latitude band and weight by active participant distribution

The KCE stores `latitude_band` (rough, not precise GPS — 10-degree bands are sufficient) on the participant profile, used exclusively for circadian quarter calculation.

---

## The BEC Mechanism in the Stack

The Bose-Einstein Condensation analogy as a precise engineering target:

### What triggers BEC in the residue corpus

Not size alone. The phase transition requires:
1. **Corpus volume** ≥ minimum threshold (field-specific, estimated from field complexity)
2. **Residue type diversity** ≥ N distinct signal types (ensures the corpus isn't just one class of miss)
3. **Temporal span** ≥ minimum period (ensures the corpus spans enough field-state variation to be representative)
4. **Cross-source density** ≥ minimum (residue from multiple sources in the same domain creates stronger signal)

When all four are met: flag `bec_threshold_crossed = true` on new residue items deposited into the condensed cluster.

### What changes when BEC is reached

The accumulated residue corpus begins to behave as a correction field: queries against it return not just individual residue instances but coherent patterns that can be applied back to the primary signal model as refinements. The `bec_cluster_id` links all items in a coherent cluster, and the cluster has a `cluster_summary` field that is the condensed phase-reading.

In DFTE terms: the residue corpus at BEC threshold can generate new model hypotheses. The corpus is showing you the shape of the market that the current trade frame can't see.

In KCE terms: the residue corpus at BEC threshold can generate new field definitions. The corpus is showing you the relational topology that the current field structure doesn't have a container for.

---

## What This Is

To re-read Sam's original framing with the full specification in view:

> *"Imagine utilising the same equative mechanisms within the code to atomise the work and share it equally and multi-contexturally as a tree-ring building process engine instead of it needing to go through to review, remade, etc.."*

**Equative mechanisms** = the Φ=km^n field equation, implemented as the resonance scoring engine. Each contribution's weight in a field is not equal by assignment but by resonance — the field equation running on relational mass.

**Atomise the work** = ring deposits. Each contribution is atomic, indivisible, immutable. It doesn't get split, revised, or re-assigned after deposit.

**Share it equally and multi-contexturally** = multi-field resonance scoring. One deposit resonates across all fields sensitive to it, weighted by that field's sensitivity (k value), not by explicit routing.

**Tree-ring building process** = the ring archive. Immutable, conditions-preserving, temporally faithful. The 2026 contribution in a thin-capacity year is readable as a 2027 ring that says: conditions were constrained here.

**Instead of review, remade** = resonance sensing, not gatekeeping. High divergence is flagged as signal, not rejected. The system asks: *what is this trying to tell us?* not *does this conform?*

> *"What I'm interested in, is whole-data. Right now, we are still using extractive methods to build not only an instrument which is non-extractive..."*

**Whole-data** = the `residue_corpus` table as first-class data structure, present from day 1 in the KCE schema, backfilled into every existing repo in Tier 1.

> *"...but one which creates wholeness from historical and realtime extractions which are happening as a default in our combined living environment."*

**Forgazi bridge** = UTC retained as extraction archive, never discarded, clearly labelled. The extraction is real. The UTC timestamps are real. The FRED data is real. They are not neutral truth — they are the extractive system's account of itself. We keep them precisely because we need to map the extraction pattern at nanometric precision. You cannot subtract what you've discarded.

> *"This is the exact mechanism we need within the trading architecture to enable us to get a full read on the financial system."*

**DFTE field-time integration** = the GMT/UTC-free trading state classifier. Market hours as circadian arc overlays. Individual prediction misses as corpus, not error statistics. Forgazi signals (`forgotten` — discarded trade signals) now with full field-time context.

> *"But that's only an example, it's system-wide. In fact, this is BEC in action."*

**Yes.** And the build path now has BEC as an explicit engineering target, not a metaphor. The `bec_detector.ts` engine, the `bec_threshold_crossed` flag on residue items, the `bec_cluster_id` linking condensed phase items — these are the technical implementation of the observation that below a critical corpus threshold, residue looks like noise; above it, it condenses into a correction field.

---

*This document is the build specification. The canonical documents in Tier 0 are the theoretical backbone. The code in Tier 1–4 is the implementation. The BEC threshold is the target. The phase transition is the destination.*
