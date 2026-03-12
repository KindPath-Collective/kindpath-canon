# BEC Detection Guide
### Recognising the Bose-Einstein Phase Transition in Accumulated Residue Corpora

*Version 1.0 — March 2026*

---

## What BEC Is — Re-stated Precisely

Bose-Einstein Condensation is a quantum phase transition that occurs when particles of integer spin are cooled below a critical temperature. Below that temperature, they stop behaving as individuals and collapse into a shared quantum ground state — the condensate. The collective behaviour becomes coherent in a way that no individual particle exhibits. The system reads itself.

The analogy is being used precisely, not metaphorically, with one important substitution: temperature maps to residue corpus diversity/density, and quantum ground state maps to the phase where accumulated residue begins to exhibit coherent structural patterns that were not visible in any individual residue item.

The analogy is exact in the following properties:
1. Individual particles (residue items) are indistinguishable at the micro level — each looks like noise
2. There is a critical threshold below which no coherent phase exists
3. The transition is not gradual — it is a phase change. Below threshold: noise. Above threshold: legible pattern.
4. Once condensed, the collective behaviour is qualitatively different from the summed behaviour of individuals

The analogy breaks at the mechanism: quantum statistics govern the particle behaviour in BEC; something more like information theory and pattern emergence governs the residue corpus. But the phenomenology — phase transition at a density threshold, with qualitatively different collective behaviour above it — is structurally identical.

---

## The Four Conditions for Phase Transition

BEC in a residue corpus does not occur from volume alone. Four conditions must be met simultaneously. All four are required. Meeting three and not the fourth will not produce a phase transition.

### Condition 1: Corpus Volume

**What it is:** The raw count of residue items in the corpus.

**Why it matters:** Phase transitions require mass. A corpus of 50 items, regardless of quality, cannot condense — there isn't enough mass for collective behaviour to emerge.

**Threshold heuristics (not hard rules):**
- Simple domain (financial price signals): ~500 individual prediction misses
- Complex domain (relational/behavioural data): ~2,000 individual items
- Cross-domain corpus: ~1,000 items per major domain included

These are not certification criteria. A corpus of 10,000 items that fails Condition 3 will not condensate. These are lower bounds below which condensation is physically impossible, not upper bounds that guarantee it.

### Condition 2: Residue Type Diversity

**What it is:** The number of distinct signal types represented in the corpus.

**Why it matters:** This is the most important condition. A corpus of 10,000 items all of the same type — say, all DFTE prediction misses in a rising market — will not condensate. The coherent pattern that emerges from BEC is the pattern of the system's actual structure as revealed by the places where the model was wrong. If all the wrongness is of one type, the pattern is clear but trivial: "this model doesn't work in rising markets." That's not a phase transition. That's a known limitation.

A corpus with high type diversity — prediction misses in rising and falling markets, during high and low volatility, during trend and ranging periods, during different geopolitical states, across different FRED series — has the multi-angle resolution needed for pattern emergence.

**Minimum viable diversity:** At least 8 distinct residue types contributing meaningfully (>5% of corpus each) to enable phase transition candidates.

**Residue types in the KindPath stack (non-exhaustive):**

| Domain | Residue Type | What it represents |
|---|---|---|
| DFTE | `prediction_miss_trending` | Model wrong in trending market |
| DFTE | `prediction_miss_ranging` | Model wrong in sideways market |
| DFTE | `forgazi_signal_suppressed` | Signal discarded by current frame |
| DFTE | `temporal_delta_miss` | Timing was wrong, not direction |
| DFTE | `fred_frame_artifact` | Apparent signal was extraction pattern artifact |
| KCE | `context_not_actioned` | Context existed, was named, not addressed |
| KCE | `edge_case_deferred` | Edge case noticed, out of scope |
| KCE | `adjacent_problem` | Adjacent problem surfaced, not chased |
| KCE | `resonance_divergence` | Deposit diverged from expected trajectory |
| KCE | `steward_interpretation_miss` | Field reading that turned out to be incomplete |
| KindSense | `reduction_layer_discard` | Signal below detection threshold |
| KindSense | `field_model_miss` | Actual field behaviour inconsistent with model |
| Kindfluence | `non_converting_interaction` | Authentic engagement that didn't convert |
| Kindfluence | `kinship_signal_missed` | Relational signal the algorithm ignored |
| kindai | `context_window_trimmed` | Context economised out of session |
| kindai | `edge_case_noted_not_actioned` | Noticed, not addressed, not tracked |
| kindpath-analyser | `creative_residue_high` | Authenticity marker that doesn't fit known fingerprints |
| kindpath-analyser | `genre_frame_miss` | Track behaviour inconsistent with genre model |

### Condition 3: Temporal Span

**What it is:** The duration over which the residue corpus was accumulated, measured in ecological time (not UTC calendar time).

**Why it matters:** A corpus accumulated in one intensive month — even if it meets volume and diversity criteria — has been accumulated within a narrow slice of field conditions. The model was wrong in consistent ways during that period. The residue pattern that emerges from it describes the model's failures under those specific conditions, not the model's structural limitations.

A corpus accumulated across two years in the Northern Rivers includes:
- Multiple seasons (the field was in different ecological states)
- Multiple market regimes (DFTE was wrong in different market conditions)
- Multiple social contexts (Kindfluence data across different cultural moments)
- Multiple life phases for the participants (contributions made in different personal seasons)

The corpus whose temporal span crosses these variations has seen the model fail in structurally diverse ways. The pattern that emerges from it is more fundamental — it describes the model's limits, not its limits in one context.

**Minimum viable temporal span:** 
- The corpus must span at least 4 ecological seasons (to catch seasonal variation)
- The corpus must include both high-activity and low-activity periods (to capture capacity variation)
- The corpus must span at least one significant disruption event in the relevant domain (financial volatility event, community transition, seasonal extreme)

### Condition 4: Cross-Source Density

**What it is:** The proportion of the corpus that comes from multiple distinct source types reaching the same unresolved patterns.

**Why it matters:** Residue from a single source, no matter how large, describes one instrument's blind spots. When DFTE price prediction residue and Kindfluence engagement residue and KindSense field model residue all contain the same pattern of unresolved signal — the same kind of behaviour that none of the current models can accommodate — that convergence is not coincidence. It is the original signal showing up in the shadow of three different extractive frames simultaneously.

Cross-source convergence is the strongest available indicator that what the residue is describing is a real structural feature of the underlying system, not an artifact of any particular model's limitations.

**Minimum viable cross-source density:**
- At least 3 distinct source repos contributing to the corpus
- At least one shared unresolved pattern type appearing independently in ≥2 source repos
- The shared pattern was not designed into the residue types (an independently emerging convergence, not a deliberate tagging overlap)

---

## Detection Algorithm

The `bec_detector.ts` engine in the KCE runs this algorithm on the `residue_corpus` table. It is also available as a standalone Python module in `kindpath-dfte` and `kindpath-analyser`.

```typescript
interface BECAssessment {
  threshold_crossed: boolean;
  confidence: number;                    // 0-1: how confident is the crossing call?
  conditions_met: {
    volume: boolean;
    diversity: boolean;
    temporal_span: boolean;
    cross_source: boolean;
  };
  
  // Only populated if threshold_crossed = true
  condensate?: {
    cluster_id: string;
    cluster_summary: string;            // Plain language: what pattern emerged?
    items_in_cluster: number;
    source_repos: string[];
    residue_types_represented: string[];
    temporal_span_days: number;
    emergence_confidence: number;       // How strongly does the pattern hold?
    field_implications: string;         // What does this mean for the model?
    next_iteration_hypothesis: string;  // What should change in the primary model?
  };
  
  // Always populated: current state toward threshold
  progress?: {
    volume_current: number;
    volume_threshold: number;
    diversity_current: number;
    diversity_threshold: number;
    temporal_span_days: number;
    temporal_span_threshold_days: number;
    cross_source_repos: string[];
    shared_patterns: string[];
    estimated_items_to_threshold: number;
  };
}

function assessBECThreshold(
  corpus: ResidueCorpus,
  domain: string
): BECAssessment { ... }
```

---

## What Changes When BEC Is Reached

This is the most important question, and the answer is often misunderstood.

**BEC does not produce a new, better primary model automatically.** It produces a **legible pattern** in the residue corpus that can inform a new iteration of the primary model. The phase transition is a precondition for next-generation model development, not a substitute for it.

**What you can do after BEC that you couldn't do before:**

1. **Query the condensate**: Ask "what does the residue corpus say about X?" and receive a coherent answer, not a distribution of individual misses. The corpus now speaks as a coherent field.

2. **Generate model hypotheses**: The condensate's `next_iteration_hypothesis` field contains the first-pass reading of what the residue corpus suggests should change. This is a hypothesis — it requires verification — but it is a structurally grounded hypothesis derived from actual model failures, not from theoretical speculation.

3. **Identify blind spots up to the threshold**: The `field_implications` field describes the structural blind spot that the current model has that produced the residue pattern. This is diagnostic: you now know specifically what the model cannot see.

4. **Route future residue more precisely**: Once a condensate exists, new residue items can be matched against it. Items that fit the condensate pattern are deposited into the known cluster. Items that don't fit become the seed of the next pre-condensation corpus — the next Phase 1.

5. **Communicate the finding**: The condensate's `cluster_summary` is plain language. It can be shared with non-technical participants, incorporated into canonical documents, and used to orient new enrollees about what the system has learned.

**What BEC does not do:**
- Automatically fix or replace the primary model
- Guarantee the next model iteration will be correct
- Produce residue from itself (the condensate is not a new model — it is a reading of the previous model's limits)
- Apply across domains automatically (a BEC threshold crossed in DFTE residue doesn't cross for KindSense residue — each corpus crosses independently)

---

## Operational Checklist

When running the BEC detector and it returns `threshold_crossed: true`:

**Immediate:**
- [ ] Archive the current pre-condensation residue corpus state (snapshot)
- [ ] Tag all items in the condensate cluster with `bec_cluster_id`
- [ ] Notify relevant field stewards and system architects
- [ ] Generate the `cluster_summary` and `field_implications` as a ring deposit in the relevant field
- [ ] Deposit `next_iteration_hypothesis` to the canon field for review

**Within one field-cycle (one ecological month):**
- [ ] Review the `next_iteration_hypothesis` with domain experts
- [ ] Develop a specific model change proposal based on the condensate reading
- [ ] Design a validation approach: how will we test whether the hypothesis is correct?
- [ ] Begin accumulation of the next residue corpus (it starts the moment the condensate forms — the current model's new residue starts immediately)

**Ongoing:**
- [ ] The primary model iteration is in progress — do not reset the residue corpus
- [ ] New residue items after BEC are tagged with `post_bec_phase: true` to distinguish the pre-condensation and post-condensation corpora
- [ ] Track whether new residue items fit the condensate cluster (validation signal) or diverge from it (new pattern emerging)

---

## False Positives

The BEC threshold can appear to be crossed prematurely. Signs of a false positive:

- **The condensate pattern is trivially obvious**: if the "pattern" is something already known and named ("this model doesn't work when volatility spikes"), the apparent condensate is probably aggregating a known category of failures, not revealing a new structural feature.

- **The cross-source condition is technically met but shallow**: two sources showing the same pattern because they were designed to produce similar residue types, not because they independently converged.

- **Temporal span condition met by calendar but not by ecological variation**: a corpus accumulated over 18 months but all in the same economic regime (e.g., a continuous bull market) doesn't truly meet the temporal span condition.

**What to do with suspected false positives:**
- Do not dismiss — the condensate may still contain valid sub-patterns
- Examine the diversity condition more carefully: are the residue types genuinely diverse in mechanism, or just in label?
- Raise the confidence threshold for `threshold_crossed: true` in the detector for this domain
- Log the false positive candidacy in the condensate record: "this may be a shallow condensation event; monitoring for stability"

---

## The Bigger Picture

The BEC threshold is not the destination. It is a waypoint.

Each condensate is the system having learned one thing it couldn't see before. The next residue corpus begins immediately. The extraction pattern map is refined. The primary model is updated. The new model has new blind spots — smaller, more precise blind spots, but still Present. The residue corpus starts again.

This is not a deficiency of the method. This is the structure of knowledge in complex systems. Every instrument has a frame. Every frame has what it can't see. The nano-mapping protocol and BEC detection are the mechanism for turning that structural reality into an asset: the things we can't see become the corpus, the corpus becomes the corrective field, the corrective field becomes the next instrument.

It is `Φ=km^n` in knowledge: mass accumulates, each condensation event is a node in the network, the network compounds, Phase 3 is not the end of accumulation but the recognition that the accumulated mass has its own energy — that the system knows things that no individual in it knows.

The organism doesn't need to understand quantum mechanics to demonstrate BEC. The flock doesn't need to understand fluid dynamics to demonstrate murmuration. The residue corpus doesn't need to be consciously managed to produce phase transitions — it needs to be **kept, honestly, at sufficient diversity and span.** The rest is physics.

---

*Reads with: `WHOLE_DATA_ACCOUNTING.md`, `THE_FIELD_EQUATION.md`, `NANO_MAPPING_PROTOCOL.md`, `KINDFIELD_COORDINATION_ENGINE_BUILD.md`*
