# kindpath-canon

Canonical methodology documents for the KindPath Collective. This repository
holds the definitive versions of the Compass methodology, trading architecture,
and practice frameworks. These documents are the source of truth referenced
by all other KindPath repositories.

## Contents

| File | Status | Description |
|------|--------|-------------|
| `THE_GROUND.md` | Active | **Read first.** The epistemological foundation beneath the canon. Negative capability, "I know that I know nothing" as positive structural claim, Gödel as formal proof of the same insight, the forgazi of the observer, and why the exponent n may be recursive and bidirectional rather than fixed. The ground beneath the other documents. |
| `COMPASS_METHODOLOGY_PENDING.md` | Pending | Compass methodology v1 (awaiting upload) |
| `TRADING_ARCHITECTURE_PENDING.md` | Pending | DFTE trading architecture |
| `practice_framework_one_pager.md` | Active | One-page practice framework reference |
| `CIRCADIAN_FIELD_MAPPING.md` | Active | The biological KindField — circadian rhythm as temporal relational health signal. Addiction as circadian colonisation. Indigenous ceremonial timing as pre-scientific circadian architecture. |
| `WHOLE_DATA_ACCOUNTING.md` | Active | The Residue-First Principle — how complete systems handle what extractive frames discard. BEC phase transition in accumulated residue. System-wide application across DFTE, KindSense, coordination engines. |
| `THE_FORGAZI_PROBLEM.md` | Active | **Foundational.** The epistemological crisis of building holistic tools entirely from extracted material. GMT/UTC as temporal colonisation chain. FRED as forgazi financial architecture. The nano-mapping response: using the extraction pattern as the subtraction tool to reconstruct original biological signal. |
| `EXECUTION_ARC.md` | Active | **Operational roadmap.** Three phases from extractive compliance to frequency resonance. The 4-cylinder/V8 power curve corrected: both are forgazi, both are F=ma. Force, Acceleration, Mass — three phase expressions of one frequency. Phase 3 is not a better engine; it is the recognition that the engines were always just a description of the frequency, not the frequency itself. |
| `THE_FIELD_EQUATION.md` | Active | **Foundational.** Φ = km^n — the master equation underlying all KindPath field descriptions. Extractive systems assume n=1. Living systems are n=2. The forgazi is the exponent gap. Instances: F=ma (n=1, navigation), F=am² and E=cm² (n=2, generative/recognition), Metcalfe's Law (n=2, network), Reed's Law (n>2, emergent). |
| `KINDFIELD_COORDINATION_ENGINE_BUILD.md` | Active | **Build specification.** The complete architecture for the KindField Coordination Engine (KCE) — the tree-ring system that replaces linear PM topology with field-resonance-deposit coordination. Includes: GMT/UTC-free temporal sovereignty module, whole-data per-repo implementation plan, new canonical documents list, Paperclip bridge strategy, BEC threshold as engineering target, and full build order Tier 0–4. |
| `TEMPORAL_SOVEREIGNTY.md` | Active | The GMT/UTC-free temporal architecture. 1884 International Meridian Conference to industrial labour time extraction to algorithmic dopamine timing. Field-time: four layers (circadian, ultradian, ecological, field-relative). Forgazi bridge for extractive-world integration. DFTE trading state as circadian arc overlay. |
| `TREE_RING_ENGINE.md` | Active | The KCE coordination model — architecture specification. Immutability, conditions-preservation, multi-contextural resonance, resonance sensing vs gatekeeping, ring archive as epistemological commitment, self-dismantling criteria. |
| `FIELD_COORDINATION_PROTOCOL.md` | Active | Practitioner guide for KCE: how to define a field, enrol participants, make a ring deposit, read the archive, and recognise the BEC threshold. Accessible to non-technical community members. |
| `NANO_MAPPING_PROTOCOL.md` | Active | Operational guide for working with forgazi data at maximum resolution. Five steps from accepting forgazi material to phase transition. Applied to DFTE, FRED ingestion, and any system reconstructing original signal from institutional data. |
| `BEC_DETECTION_GUIDE.md` | Active | How to recognise the BEC threshold in any residue corpus: volume, diversity, temporal span, cross-source density. What changes operationally when Phase 3 is reached. |

## Per-Repo Implementations

The following modules implement the KCE / temporal sovereignty / BEC model across
the KindPath codebase. Each was built per the `KINDFIELD_COORDINATION_ENGINE_BUILD.md` spec.

### kindpath-dfte
| File | Status | Description |
|---|---|---|
| `dfte/residue_logger.py` | Active | SQLite residue log; deposits trade-step residue to `trade_residue` table with temporal context |
| `dfte/field_time_bridge.py` | Active | Python twin of KCE temporal bridge — Spencer formula, 5-quarter circadian, 8-point seasons, forgazi UTC reference |
| `dfte/global_circadian_trading_state.py` | Active | 11-region global arc computation; weights circadian state across global market activity |
| `dfte/residue_backtest.py` | Active | Backtest residue accumulation → BEC threshold detection over historical trade data |

### KindSense
| File | Status | Description |
|---|---|---|
| `src/kindearth/residue_logger.py` | Active | Attaches field-residue logging to KindEarth metric field observations; deposits to `field_residue` table |

### Kindfluence
| File | Status | Description |
|---|---|---|
| `src/kindfluence/interaction_corpus.py` | Active | Interaction residue corpus builder; BEC threshold detection across Kindfluence engagement data |
| `src/kindfluence/__init__.py` | Active | Updated exports for interaction_corpus module |

### kindai
| File | Status | Description |
|---|---|---|
| `core/session.py` | Active | Extended with `session_residue` table, `SessionResidue` dataclass, `log_residue()`, `get_residue_corpus()`, `check_bec_threshold()` methods |

### kindpath-analyser
| File | Status | Description |
|---|---|---|
| `core/residue_bridge.py` | Active | Bridges analyser features to KCE residue format; `ResidueDeposit` dataclass + `extract_residue_from_analysis()` |
| `core/temporal_context.py` | Active | Python `TemporalContext` dataclass matching KCE schema; `build_temporal_context()` + helper functions |

### kindpath-kce (new repo)
| File | Status | Description |
|---|---|---|
| `package.json`, `tsconfig.json`, `drizzle.config.ts` | Active | TypeScript/Express/Drizzle setup, port 7870 |
| `src/schema/*.ts` | Active | 6 Drizzle ORM schemas: fields, ring_deposits, participants, residue_corpus, bec_condensates, temporal_contexts, resonance_events |
| `src/temporal/temporal_context.ts` | Active | All TypeScript types: `CircadianQuarter`, `EightPointSeason`, `LunarPhase`, `TemporalContext`, `GlobalCircadianTradingState`, `BECAssessment` |
| `src/temporal/field_time_bridge.ts` | Active | `buildTemporalContext()`, Spencer solar formula, lunar phase, ecological seasons, forgazi UTC reference |
| `src/temporal/circadian_engine.ts` | Active | `computeGlobalCircadianState()` — 11-region arc with weights (London 35%, NYC 25%, etc.) |
| `src/engine/bec_detector.ts` | Active | `detectBEC()` — 4-condition BEC threshold check + condensate computation |
| `src/engine/resonance_engine.ts` | Active | `scoreResonance()` — LSII-style 4-axis weighted divergence score |
| `src/api/server.ts` | Active | Express REST API: /health, /temporal/*, /fields/*, /participants/*, /residue/* |
| `src/bridge/paperclip_bridge.ts` | Active | Paperclip → KCE conversion layer; `buildBatchImportPayload()` |
| `src/index.ts` | Active | Public exports |
| `drizzle/0001_initial.sql` | Active | Raw SQL migration with all tables and indexes |
| `README.md`, `AGENTS.md` | Active | Repo documentation |

---

## Rules

- Changes here may require updates in `kindpath-fieldkit`, `kindpath-compass`, and practitioner materials.
- Mark any pending or unverified documents clearly (e.g. `_PENDING.md` suffix).
- Follow KindPath doctrine: benevolence, syntropy, sovereignty.

## Related

- [kindpath-fieldkit](https://github.com/KindPath-Collective/kindpath-fieldkit) — public working materials
- [kindpath-compass](https://github.com/KindPath-Collective/kindpath-compass) — practice aid for compassionate listening
