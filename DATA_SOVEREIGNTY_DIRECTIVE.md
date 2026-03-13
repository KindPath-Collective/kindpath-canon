# Data Sovereignty Directive
### The KindPath Standard for Data Governance, Public Accountability, and Independent Audit

*Version 1.0 — March 2026*
*Status: Active — Binding across all KindPath Collective operations*

---

## Preamble

Data collection is not a neutral act. In the current economic environment, "data governance" is most commonly a compliance exercise — a floor, not a ceiling. Industry standards are frequently industry minimums. They describe the least that must be done to avoid liability, not the most that can be done to honour the people whose lives generate the data.

KindPath operates from a different premise entirely.

We collect data because we are a research instrument. The signal we gather — relational, economic, creative, ecological — is the basis of everything we build. That creates an obligation that cannot be discharged by compliance alone. The people whose signal flows through this system are not data subjects. They are the reason the system exists. Their sovereignty over their own signal is not a regulatory requirement. It is a founding principle.

This directive is the operational expression of that principle. It is not aspirational. Every commitment stated here is binding from the date of adoption. Where implementation is pending, a delivery date is stated. Where an external partner commitment is confirmed, it is named. Where a commitment is targeted but not yet finalised, it is marked **[TARGETED — Sam to confirm]**.

Trust is not claimed. It is demonstrated, repeatedly, in public, before it is needed.

---

## The Three-Part Standard

KindPath holds itself to three simultaneous and independent accountability layers. These are not sequential or interchangeable. All three must be active at all times.

### 1. Daily Public Self-Audit

Every operational day, KindPath publishes a Data Health Log. This is not a marketing summary. It is a machine-readable and human-readable record of:

- What data was collected that day, by category, across all active services
- What data was deleted or expired per retention policy
- Any access requests received and their resolution status
- Any anomalies, breaches, or near-misses detected — including minor ones
- The status of each active data processing system (operational / degraded / suspended)

The log is committed to a public GitHub repository under `kindpath-data-governance/` no later than 23:59 AEST each operational day. It is signed with a PGP key whose public key is published on the KindPath website.

Gaps in the log are not acceptable. If a gap occurs, the next log must include an explanation. The community holds us to this — not through a reporting mechanism, but because the record is permanently public and chronologically verifiable.

This public self-audit is the minimum standard. It does not replace independent verification.

### 2. Independent International Audit — Minimum Two Per Year

No organisation can audit itself into trustworthiness. Self-reporting is necessary but structurally insufficient. Independent external audit is not a supplement to self-audit — it is a separate and irreplaceable accountability mechanism.

KindPath commits to a minimum of **two independent international standards audits per year**, conducted by organisations with no commercial relationship with KindPath, under different frameworks, reporting findings publicly in full.

Audit partner status is maintained in **Schedule A** below. As of this version, no partners are yet contractually confirmed. Outreach is active and publicly tracked until confirmation is complete.

In addition to the independent audits, KindPath complies with all applicable statutory obligations under Australian law, including reporting requirements to the OAIC and ACNC governance standards once registered.

### 3. Statutory Compliance — The Floor, Not the Ceiling

Statutory compliance is the minimum legal requirement. KindPath meets it completely. It does not define the KindPath standard.

Applicable frameworks:
- **Privacy Act 1988 (Cth)** and the **Australian Privacy Principles (APPs)** — all 13 principles, in full, with no reliance on small business exemptions
- **ACNC Governance Standards** — once NFP registration is complete, all five standards maintained permanently
- **GDPR (EU)** — applied to all data involving persons in the EU, and used as the baseline for all data handling globally regardless of jurisdiction, because it is the strongest statutory individual rights framework currently in force at scale
- **CARE Principles for Indigenous Data Governance** (Collective Benefit, Authority to Control, Responsibility, Ethics) — applied to all data involving First Nations communities or practitioners, with specific protocols maintained in the practitioner field guide

Statutory compliance is verified annually by a qualified legal practitioner and confirmed in the annual statutory audit report, published publicly.

---

## The Data Sovereignty Framework

### What We Collect and Why

KindPath collects signal in the following categories:

| Category | What It Is | Why | Retention |
|---|---|---|---|
| Relational signal | Anonymised patterns of relational interaction within KCE | Field research — understanding how communities coordinate | 7 years, anonymised |
| Economic signal | DFTE/KEPE market signal (public data sources) | Trading engine calibration | Indefinite — public data |
| Creative signal | Audio analysis outputs (no raw audio retained) | Analyser seedbank and research corpus | Indefinite — with participant consent |
| Case coordination signal | NDIS case note data | Service delivery — NDIS compliance | 7 years — encrypted at rest |
| Practitioner signal | Session data from KindPath Compass | Practice support and methodology improvement | Session-only unless consented |
| Operational signal | System logs, error logs | Security and reliability | 90 days |

This table is versioned. Any addition to this table requires a governance vote and is published 30 days before the new collection begins.

### What We Do Not Do — Non-Negotiable Prohibitions

These are not policies that can be overridden by commercial pressure, partnership terms, or operational convenience. They are structural.

1. **We do not sell data.** No participant data, no aggregate data, no derived insights about identifiable individuals or communities, to any third party, under any commercial arrangement, ever.

2. **We do not license data.** No data licensing arrangements, API monetisation of participant signal, or "research partnerships" that give external organisations access to participant-level data.

3. **We do not use dark patterns.** No consent flows designed to obscure what is being agreed to. No bundled consent. No pre-checked boxes. No consent buried in terms of service. Every consent is granular, plain-language, and separately obtained per data category.

4. **We do not retain beyond stated periods.** Retention schedules are not suggestions. They are automated and logged. Any retention beyond schedule requires a documented exception with community notification.

5. **We do not operate in the grey.** When a data handling question is ambiguous under law, we apply the interpretation most protective of participant rights — not the interpretation most operationally convenient for us.

### Individual Participant Rights

Every person whose data flows through any KindPath system holds the following rights, exercisable at any time, without fees or delays beyond 30 days:

- **Right to know** — a complete, plain-language description of what data we hold about them
- **Right to access** — a machine-readable export of all data we hold about them
- **Right to correction** — amendments to any inaccurate data, with a correction log retained
- **Right to deletion** — complete erasure from all systems, including backups, within 30 days. Exceptions only where retention is required by law, clearly stated at the time of the deletion request.
- **Right to portability** — their data in a format they can take to another system
- **Right to object** — to any specific processing activity, with effect immediate upon receipt

These rights are exercised by contacting privacy@kindpathcollective.org. Every request is logged publicly (with PII stripped) in the Data Health Log.

---

## Standards Framework

KindPath aligns with the following frameworks. Alignment means we read and apply the full standard, not just the headline requirements.

| Standard | Body | Scope |
|---|---|---|
| ISO/IEC 27001:2022 | ISO | Information security management |
| ISO/IEC 27701:2019 | ISO | Privacy information management (PIMS) |
| ISO/IEC 29100:2011 | ISO | Privacy framework |
| MyData Global Principles | MyData Global | Human-centric personal data |
| Open Data Institute Open Data Certificate | ODI (UK) | Responsible open data publishing |
| IEEE 7000-2021 | IEEE | Ethics in system design |
| CARE Principles | Global Indigenous Data Alliance | Indigenous data governance |
| GDPR (as global baseline) | EU | Individual rights framework |
| Australian Privacy Principles | OAIC | Statutory privacy obligations |

ISO certification is a target for the 2027 fiscal year. Until formal certification, alignment is self-assessed quarterly and independently verified in the annual audit schedule.

---

## Schedule A — Audit Partner Status

Status date: 2026-03-13

As of this date, there are **no contractually confirmed Schedule A audit partners yet**. This does not change the binding commitment of minimum two independent international audits per year. It means the commitment is in active partner-acquisition phase.

### Confirmation table (updates when signed)

| Partner | Framework | Last Audit | Next Scheduled | Report Published |
|---|---|---|---|---|
| _None confirmed yet_ | | | | |

### Active outreach tracker

| Partner | Focus | Outreach Status | Notes |
|---|---|---|---|
| Open Data Institute (UK) | Open data governance assessment | Outreach pack prepared (2026-03-13) | Pending direct send and scoping call |
| MyData Global | Human-centric data rights assessment | Outreach pack prepared (2026-03-13) | Pending direct send and scoping call |
| Australian Information Industry Association (AIIA) | Digital ethics governance review | Outreach pack prepared (2026-03-13) | Pending direct send and scoping call |
| KPMG Digital Trust (Australia) | Privacy/cyber assurance review | Outreach pack prepared (2026-03-13) | Pending direct send and scoping call |

### Targeted Partners — Not Yet Confirmed

The following organisations have been identified as appropriate independent audit partners. Engagement is being pursued.

- **Open Data Institute (UK)** — Open Data Certificate and responsible data practice assessment
- **MyData Global** — Human-centric data ethics audit aligned with the MyData Principles
- **Australian Information Industry Association (AIIA)** — Digital Ethics assessment
- **KPMG Digital Trust (Australia)** — Privacy and data governance assurance

Confirmed partnerships are moved into the confirmation table above with signed dates, review scope, and public report links.

---

## NFP Application Integration

The data sovereignty framework described in this directive is core evidence for KindPath's NFP and potential Deductible Gift Recipient (DGR) application to the ACNC and ATO. The following elements directly support the application:

**Public benefit test:** The daily public self-audit, open seedbank (kindpath-analyser), and open methodology (kindpath-canon, kindpath-fieldkit) are forms of public benefit that benefit a class of persons beyond KindPath's direct participants. The research conducted under this framework contributes to public knowledge about data sovereignty, relational economics, and creative authenticity.

**Accountability:** The ACNC Governance Standards require NFPs to operate responsibly and accountably. This directive, its public audit trail, and its independent audit schedule constitute pre-established governance infrastructure that exceeds ACNC requirements.

**Financial controls:** KindPath's prohibition on data commercialisation aligns with the NFP requirement that activities not be for the profit of members. No revenue is generated from participant data under any circumstances.

The NFP application should reference this document directly and include the most recent published Data Health Logs and any available independent audit reports as supporting evidence.

---

## Governance and Amendments

This directive is a living document. It may be strengthened — commitments added, standards raised, audit cadence increased — but it may not be weakened without:

1. A 90-day public notice period
2. An explanation of the reason for any reduction in commitment
3. Community consultation via a published RFC (Request for Comment)
4. Sam's explicit written approval

The version history of this document is permanently maintained in the `kindpath-canon` git repository. No version is ever deleted.

This directive is reviewed in full every six months and updated to reflect current operational reality, confirmed partnerships, and any audit findings that require policy response.

---

*KindPath Collective — Data Sovereignty Directive v1.0*
*Adopted: March 2026*
*Next review: September 2026*
*Maintained by: Samuel Cross, KindPath Collective*
*Questions: privacy@kindpathcollective.org*
