# TASKS — wash-guides (open water, sanitation & hygiene how-tos)

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## How these tasks map to Elyos

Each task below becomes an Elyos **Task JSON** validated against
`packages/schema/src/schemas.ts`. Field mapping:

- `id` — stable slug ID, e.g. `wash-guides-arch-001`.
- `title` — the task title from the table.
- `project` — `"wash-guides"`.
- `type` — one of `code | research | writing | data | design-spec | maintenance` (the "Type" column).
- `lane` — `"donated"` for all tasks here (no escrow/API spend). A `funded` task would require
  `fundedBudgetUsd`.
- `priority` — `high | medium | low`.
- `domain` — array, e.g. `["public-health","wash","content","accessibility","translation"]`.
- `riskTier` — `low | medium | high` (the "Risk" column). General hygiene/sanitation content is
  **medium**; ORS/dehydration and chemical water-treatment **dosing** content is **high**.
- `urgent` — boolean (default `false`; this is reference/prevention content, not live response).
- `deliverable` — `pr | dataset | document | translation` (the "Deliverable" column).
- `tokenEstimate` — `small | medium | large` (the "Size" column).
- `status` — `open | in-progress | review | delivered | done` (all start `open`).
- `context`, `objective`, `acceptanceCriteria[]`, `output` — task narrative + checkable criteria.
- `resources[]` — source/reference URLs or repo paths.
- `requestor` — partner/requestor (**TO BE SECURED**; use `"TBD"` until a partner is named).
- `verifiedNeed` — **`false` until a named partner org confirms need in writing** (honest default).
- `outputLicense` — `"MIT"` for code/tooling, `"CC-BY-4.0"` for content/translations.

**Reviewer column legend:** `maintainer` (code/schema review), `content/WASH` (WASH/public-health
domain reviewer for medium-risk content), `expert/HIGH` (credentialed expert — WASH/environmental-
health professional for dosing, licensed clinician for ORS/dehydration — **TO BE SECURED**),
`numeric` (independent numeric second-checker, not the author), `a11y` (accessibility reviewer),
`translation+safety` (competent speaker paired with safety-accuracy re-check), `cultural` (cultural/
dignity reviewer for sanitation/MHH).

**Core review rules.**
- **No self-approval:** for every content task, `reviewedBy` (author) and `approvedBy` must be distinct
  people; build validation rejects `approvedBy == reviewedBy`.
- **HIGH-risk gate (`riskTier: high`):** a unit may not ship without (a) recorded credentialed
  **`expertSignOff`** (version-scoped), (b) **independent numeric verification** of every dose/ratio/
  contact-time (`numericClaims[].verifiedBy` ≠ author, `expertConfirmed: true`), and (c) the persistent
  **"informational, not a substitute for professional care/training"** disclaimer + danger-sign/when-
  to-seek-care content. CI fails any HIGH unit missing these. **No expert secured ⇒ no HIGH tasks
  start; the project holds at M1.**
- **License/provenance rule:** paraphrase + cite, **never** copy source text or reproduce logos/emblems;
  verify and record each source's license before ship (WHO content is `CC BY-NC-SA 3.0 IGO` —
  non-relicensable; facts paraphrased + cited only).

**Sequencing rule (M0):** the **content-format ADR (`arch-001`) is decided first**; the content schema
(`data-003`) and renderer depend on it and are provisional until it lands. The **risk-classification
policy (`arch-002`)** is decided in M0 and gates which units enter M2.

---

## Milestone M0 — Foundation & cold-start

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| wash-guides-arch-001 | ADR: content format (JSON vs MDX) — **decide first** | design-spec | small | low | document | — | maintainer |
| wash-guides-arch-002 | ADR: risk-classification policy (which topics are HIGH; gates each triggers) | design-spec | small | medium | document | — | maintainer, content/WASH |
| wash-guides-data-003 | Content-unit schema + provenance/review-log + numeric-claim record | data | medium | low | dataset | arch-001, arch-002 | maintainer, content/WASH |
| wash-guides-ci-004 | CI gates: schema validation, citation-coverage, no-self-approval, numeric-verification, readability, copy/similarity, no-egress | code | medium | low | pr | data-003 | maintainer |
| wash-guides-style-005 | Plain-language style guide + controlled vocabulary | writing | small | low | document | — | content/WASH, a11y |
| wash-guides-content-006 | Sample medium-risk unit: handwashing technique + critical times (source-cited) | writing | small | medium | document | data-003, style-005 | content/WASH |

**Acceptance criteria — key tasks**

- **wash-guides-arch-002 (risk-classification policy):**
  - Documents the explicit rule that clinical (ORS/dehydration danger-signs) and chemical-dosing
    (chlorination concentrations/contact times, SODIS conditions) topics are `riskTier: high`; general
    hygiene/sanitation behavior is `medium`.
  - Specifies the gates each class triggers (medium: domain review + no self-approval; high: + expert
    sign-off + numeric verification + "not a substitute" framing + danger-signs).
  - Defines the scope boundary (safe household practice vs. out-of-scope clinical instruction) with the
    known borderline cases flagged for the credentialed expert to confirm.
- **wash-guides-data-003 (content schema):**
  - Captures `topic`, `riskClass`, localized `title`/`steps`, `audience`, `numericClaims[]`
    (value/unit/context/sourceRef/verifiedBy/expertConfirmed), `sources[]`
    (org/title/url/retrievedDate/sourceLicense/licenseVerified), `reviewStatus`, `reviewedBy`,
    `approvedBy` (distinct), `expertSignOff?` (required when `riskClass:high`), `reviewLogRef`,
    `disclaimer`, `lang`, `contentLicense`, `contentVersion`, `lastReviewed`, `validUntil`.
  - Follows the content-format ADR (arch-001); provisional until that ADR lands.
  - Build validation rejects: missing citation/review fields; `approvedBy == reviewedBy`; a `high` unit
    with no `expertSignOff`; any `numericClaim` lacking `verifiedBy`/`expertConfirmed`; a source with
    `licenseVerified:false`.
- **wash-guides-ci-004 (CI gates):**
  - Runs schema validation, citation-coverage (100% of claims cited), no-self-approval, numeric-
    verification (every numeric claim second-checked), readability (target reading level), copy/
    similarity check (flags verbatim source reuse), and — for any rendered output — a11y + no-egress
    (CSP `connect-src 'none'` + runtime network-interception). `pnpm build && pnpm test && pnpm lint`
    pass.
- **wash-guides-content-006 (handwashing sample, medium):**
  - Every claim traceable to a cited authoritative source (WHO/UNICEF/CDC) with retrieval date + verified
    license; **paraphrased, no copied text, no logos/emblems**.
  - Plain-language, low-literacy-friendly steps per the style guide.
  - Passes content/WASH review by an approver **distinct from the author**; PR-tied review-log entry
    written. No clinical instruction (medium-risk topic only).

**Definition of Done (M0):** content-format + risk-classification ADRs recorded; content schema +
provenance/review-log + numeric-claim record defined; CI enforces validation/citation/no-self-approval/
numeric/readability/copy/no-egress gates; plain-language style guide published; one medium-risk,
source-cited, paraphrased, domain-reviewed handwashing unit exists. **No HIGH-risk content in M0.**

---

## Milestone M1 — Core medium-risk content + renderer

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| wash-guides-render-007 | Static, offline-friendly renderer: accessible HTML + printable output + disclaimer/attribution | code | large | low | pr | data-003 | maintainer, a11y |
| wash-guides-content-008 | Safe water storage + boiling water units (source-cited) | writing | medium | medium | document | content-006 | content/WASH |
| wash-guides-content-009 | SODIS + household filtration + settling/flocculation units (method-level, no dosing) | writing | medium | medium | document | content-006 | content/WASH |
| wash-guides-content-010 | Sanitation: latrine use/maintenance + safe disposal of child feces | writing | medium | medium | document | content-006 | content/WASH, cultural |
| wash-guides-content-011 | Menstrual health & hygiene (MHH) unit | writing | medium | medium | document | content-006 | content/WASH, cultural |
| wash-guides-content-012 | Household cleaning & surface disinfection (non-clinical) | writing | small | medium | document | content-006 | content/WASH |
| wash-guides-a11y-013 | WCAG 2.2 AA hardening + manual AT audit of rendered site | code | medium | low | pr | render-007 | a11y |

**Acceptance criteria — key tasks**

- **wash-guides-render-007 (renderer):**
  - Emits accessible HTML and print-optimized output that works **offline** with no network egress
    (CSP `connect-src 'none'`; runtime no-egress E2E).
  - Every rendered unit shows attribution, source citations, and the risk-appropriate disclaimer,
    including the "not an official/endorsed WHO/UNICEF/CDC product" notice.
  - No third-party logos/emblems, trackers, or analytics; TypeScript/ESM; builds via pnpm.
- **wash-guides-content-009 (SODIS/filtration/flocculation):**
  - Method-level guidance only (conditions, technique); any chemical **dosing** (e.g., flocculant or
    chlorine amounts) is split into the HIGH-risk M2 units, not embedded here.
  - Every claim source-cited + paraphrased; reviewed by an approver distinct from the author.
- **wash-guides-content-010 / -011 (sanitation / MHH):**
  - Passes both content/WASH accuracy review **and** cultural/dignity review (gender-sensitive,
    non-stigmatizing); within scope (no clinical instruction).
- **wash-guides-a11y-013 (AA hardening):**
  - Automated axe/pa11y pass with 0 critical issues; documented manual AT audit across a defined
    support matrix; printable output legible and low-literacy-friendly.

**Definition of Done (M1):** ≥ 8 medium-risk topics authored, source-cited, paraphrased, and reviewed
(handwashing, safe water storage, boiling, SODIS, filtration, latrine use/maintenance, safe disposal of
child feces, surface disinfection; MHH where culturally reviewed); renderer emits accessible, printable,
offline output with attribution + disclaimer; WCAG 2.2 AA pass; no-egress + provenance/license audits
green. **No HIGH-risk content shipped yet.**

---

## Milestone M2 — HIGH-risk content (expert-gated)

> **Hard gate:** no task in M2 starts until a **credentialed expert reviewer is secured** (outreach
> deadline 2026-09-30). If unmet, the project holds at M1.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| wash-guides-partner-014 | Secure credentialed expert reviewer(s): WASH/EH + clinician | research | medium | medium | document | — | maintainer, steward |
| wash-guides-content-015 | ORS preparation + dehydration danger-signs / when-to-seek-care (clinical) | writing | medium | **high** | document | partner-014, data-003 | expert/HIGH (clinician), numeric, content/WASH |
| wash-guides-content-016 | Household chlorination: concentration + contact time dosing | writing | medium | **high** | document | partner-014, content-008 | expert/HIGH (WASH/EH), numeric, content/WASH |
| wash-guides-content-017 | Chemical disinfection dosing for flocculation/SODIS edge conditions | writing | small | **high** | document | partner-014, content-009 | expert/HIGH (WASH/EH), numeric |
| wash-guides-ci-018 | Enforce HIGH-risk gate in CI (expertSignOff + numeric verification + disclaimer required) | code | small | low | pr | data-003 | maintainer |

**Acceptance criteria — key tasks**

- **wash-guides-partner-014 (secure expert):**
  - A WASH/environmental-health professional (dosing) **and** a licensed clinician (ORS/dehydration)
    agree to review, with credentials + consent recorded in a reviewers ledger; version-scoped sign-off
    and veto/escalation rules acknowledged.
  - On success, HIGH-risk tasks (content-015..017) may begin; until then they remain blocked.
- **wash-guides-content-015 (ORS + dehydration danger-signs, HIGH):**
  - Every numeric value (ORS ratio/volumes, timings) is tied to a **specific** cited authoritative
    source, **independently second-checked** by `numeric` (≠ author), and **expert-confirmed** by the
    clinician (`expertConfirmed:true`).
  - Includes explicit **danger-signs / when-to-seek-care** content and the persistent **"informational,
    not a substitute for professional medical care"** disclaimer.
  - Stays within scope: no diagnosis, no medication/IV instruction; borderline cases (e.g., infants)
    handled per the expert-confirmed scope line; links out to care.
  - Recorded `expertSignOff` (version-scoped) before merge; CI HIGH-gate green; review-log entry written.
- **wash-guides-content-016 (chlorination dosing, HIGH):**
  - Concentrations and contact times tied to specific cited sources, numeric-verified, and
    expert-confirmed by the WASH/EH reviewer; where authorities diverge on a value, divergence is stated
    and both linked (not averaged).
  - "Informational, not a substitute for trained WASH practice" disclaimer present; safe-handling
    cautions for chlorine included; no brand/product recommendation.
- **wash-guides-ci-018 (HIGH-risk CI gate):**
  - Build **fails** any `riskTier:high` unit lacking `expertSignOff`, with any `numericClaim` missing
    `verifiedBy`/`expertConfirmed`, or missing the required disclaimer/danger-sign fields.

**Definition of Done (M2):** ORS/dehydration + chemical-dosing units shipped **only** with credentialed-
expert sign-off, independent numeric verification, "not a substitute" framing, and danger-sign content;
CI HIGH-gate enforced; scope guardrail (no clinical treatment instruction) holds.

---

## Milestone M3 — i18n & localization

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| wash-guides-i18n-019 | i18n framework: catalogs, safe fallback, RTL, bundled offline fonts, completeness check | code | medium | low | pr | render-007 | maintainer, a11y |
| wash-guides-l10n-020 | Localize core medium-risk set into priority language #1 (safety-accuracy reviewed) | writing | large | medium | translation | i18n-019, content-012 | translation+safety, content/WASH |
| wash-guides-l10n-021 | Localize HIGH-risk units into priority language #1 (numeric re-verified per language) | writing | medium | **high** | translation | l10n-020, content-016 | translation+safety, expert/HIGH, numeric |
| wash-guides-l10n-022 | Localize core set into priority language #2 (safety-accuracy reviewed) | writing | large | medium | translation | i18n-019, content-012 | translation+safety, content/WASH |

**Acceptance criteria — key tasks**

- **wash-guides-i18n-019 (i18n framework):**
  - Strings/units externalized; locale negotiation falls back safely to a verified language (never blank
    or broken safety text); RTL layout supported where a target language needs it; offline fonts bundled
    with required glyph coverage (no runtime web-font fetch); build-time completeness check.
- **wash-guides-l10n-021 (HIGH-risk localization):**
  - Translation safety-accuracy reviewed (numbers/doses/danger-signs/step order), **numeric values
    re-verified in the target language**, and expert spot-checked where feasible; disclaimer + danger-
    signs preserved; `contentLicense: CC-BY-4.0`; source attribution preserved.

**Definition of Done (M3):** i18n framework with completeness + safe fallback; ≥ 2 non-English locales
for the core set; any localized HIGH-risk unit re-verified numerically and safety-reviewed in-language;
RTL exercised if a target language requires it.

---

## Milestone M4 — Partner adoption & field validation (the deed)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| wash-guides-partner-023 | Secure named WASH/health distribution partner (need, topics, languages, endorsement) | research | medium | medium | document | — | maintainer, steward |
| wash-guides-deploy-024 | Production publish: static site + printable packs + versioning/staleness + disclaimers | code | medium | low | pr | a11y-013, i18n-019 | maintainer, steward |
| wash-guides-ops-025 | Outcomes-tracking process (partner self-report) + content re-review cadence + staleness fail-safe | maintenance | small | low | document | partner-023 | maintainer, steward |

**Acceptance criteria — key tasks**

- **wash-guides-partner-023 (secure partner):**
  - A named WASH/health org confirms need in writing (letter of support / MOU), identifies priority
    topics + languages, and agrees to adopt/distribute. On success, `verifiedNeed` flips to `true` and
    `requestor` is set to the named org across the project's tasks.
- **wash-guides-deploy-024 (production publish):**
  - Static build deployed over HTTPS; printable packs generated; versioned content with `validUntil`
    staleness fail-safe (HIGH units past window withheld until re-signed-off); visible "not an official/
    endorsed product" disclaimer + attribution; no telemetry/PII (no-egress verified).
- **wash-guides-ops-025 (outcomes + freshness):**
  - Privacy-preserving outcomes process (partner self-report; no in-app telemetry) using a standard
    template (partner, period, channels, **distinct people/households reached (confirmed)**, flagged
    estimates, regions/languages, de-dup notes) over a rolling 12-month window; counts distinct
    recipients (not downloads), once per period across touchpoints, de-duplicated across partners at
    roll-up. Re-review cadence defined (shorter for HIGH units); stale-content flagging via
    `lastReviewed`/`validUntil`.

**Definition of Done (M4 / Definition of Shipped, partner-adopted):** a named WASH/health partner
endorses/distributes the content in their community's language(s) (`verifiedNeed:true`); all HIGH units
carry expert sign-off + numeric verification + framing; provenance/license clean; accessible + printable
+ offline; no telemetry/PII; outcomes tracking + re-review cadence operational.

**Decision point (so finished content isn't stranded):** if no partner is secured by **~2027-03-31**,
the steward + Elyos governance declare **"Publicly Shipped (generic public good)"** — criteria (1)–(5)
of the *Definition of Shipped* met, published and distributed directly/via community channels, outcomes
tracked by best-effort self-report. A later partner adoption upgrades the status to "partner-adopted."
HIGH-risk units remain part of a shipped state **only** with expert sign-off + numeric verification.

---

## Backlog / future

| ID | Title | Type | Size | Risk | Deliverable | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| wash-guides-content-026 | Hygiene in outbreaks/displacement (household-level cholera prevention) | writing | medium | high | document | Expert-gated; danger-signs + "not a substitute" framing |
| wash-guides-content-027 | Safe water for the immunocompromised (household practice) | writing | small | high | document | Clinician sign-off |
| wash-guides-design-028 | Low-literacy pictogram set (openly-licensed or original) | design-spec | medium | low | document | License-clean assets only; no emblems |
| wash-guides-l10n-029 | Additional priority languages (low-resource focus) | writing | large | medium | translation | Safety-accuracy + numeric re-verify per language |
| wash-guides-content-030 | School-WASH hygiene-promotion pack | writing | medium | medium | document | Partner/context-driven |
| wash-guides-ops-031 | Annual re-validation against updated WHO/UNICEF/CDC guidance | maintenance | medium | medium | document | Recurring; shorter cadence for HIGH units |
| wash-guides-sec-032 | Dependency/supply-chain audit + SRI hardening | maintenance | small | low | pr | Recurring |
| wash-guides-content-033 | Read-aloud/audio versions for non-readers | writing | medium | low | document | Pairs with low-literacy goal |

---

## Generated task index

> Auto-generated by the Elyos task-decomposition agent on 2026-06-29. One JSON file per backlog row;
> seeds kept. Validation: `node validate-tasks.mjs tasks/` → **33 files, ALL VALID**.

| File | Title | Type | Size | Risk | Deliverable | Status |
| --- | --- | --- | --- | --- | --- | --- |
| tasks/wash-guides-arch-001.json | ADR: content format (JSON vs MDX) — decide first | design-spec | small | low | document | open |
| tasks/wash-guides-arch-002.json | ADR: risk-classification policy (which topics are HIGH; gates each triggers) | design-spec | small | medium | document | open |
| tasks/wash-guides-data-003.json | Content-unit schema + provenance/review-log + numeric-claim record | data | medium | low | dataset | open |
| tasks/wash-guides-ci-004.json | CI gates: schema validation, citation-coverage, no-self-approval, numeric-verification, readability, copy/similarity, no-egress | code | medium | low | pr | open |
| tasks/wash-guides-style-005.json | Plain-language style guide + controlled vocabulary | writing | small | low | document | open |
| tasks/wash-guides-content-006.json | Sample medium-risk unit: handwashing technique + critical times (source-cited) | writing | small | medium | document | open |
| tasks/wash-guides-render-007.json | Static, offline-friendly renderer: accessible HTML + printable output + disclaimer/attribution | code | large | low | pr | open |
| tasks/wash-guides-content-008.json | Safe water storage + boiling water units (source-cited) | writing | medium | medium | document | open |
| tasks/wash-guides-content-009.json | SODIS + household filtration + settling/flocculation units (method-level, no dosing) | writing | medium | medium | document | open |
| tasks/wash-guides-content-010.json | Sanitation: latrine use/maintenance + safe disposal of child feces | writing | medium | medium | document | open |
| tasks/wash-guides-content-011.json | Menstrual health & hygiene (MHH) unit | writing | medium | medium | document | open |
| tasks/wash-guides-content-012.json | Household cleaning & surface disinfection (non-clinical) | writing | small | medium | document | open |
| tasks/wash-guides-a11y-013.json | WCAG 2.2 AA hardening + manual AT audit of rendered site | code | medium | low | pr | open |
| tasks/wash-guides-partner-014.json | Secure credentialed expert reviewer(s): WASH/EH + clinician | research | medium | medium | document | open |
| tasks/wash-guides-content-015.json | ORS preparation + dehydration danger-signs / when-to-seek-care (clinical) | writing | medium | **high** | document | open |
| tasks/wash-guides-content-016.json | Household chlorination: concentration + contact time dosing | writing | medium | **high** | document | open |
| tasks/wash-guides-content-017.json | Chemical disinfection dosing for flocculation/SODIS edge conditions | writing | small | **high** | document | open |
| tasks/wash-guides-ci-018.json | Enforce HIGH-risk gate in CI (expertSignOff + numeric verification + disclaimer required) | code | small | low | pr | open |
| tasks/wash-guides-i18n-019.json | i18n framework: catalogs, safe fallback, RTL, bundled offline fonts, completeness check | code | medium | low | pr | open |
| tasks/wash-guides-l10n-020.json | Localize core medium-risk set into priority language #1 (safety-accuracy reviewed) | writing | large | medium | translation | open |
| tasks/wash-guides-l10n-021.json | Localize HIGH-risk units into priority language #1 (numeric re-verified per language) | writing | medium | **high** | translation | open |
| tasks/wash-guides-l10n-022.json | Localize core set into priority language #2 (safety-accuracy reviewed) | writing | large | medium | translation | open |
| tasks/wash-guides-partner-023.json | Secure named WASH/health distribution partner (need, topics, languages, endorsement) | research | medium | medium | document | open |
| tasks/wash-guides-deploy-024.json | Production publish: static site + printable packs + versioning/staleness + disclaimers | code | medium | low | pr | open |
| tasks/wash-guides-ops-025.json | Outcomes-tracking process (partner self-report) + content re-review cadence + staleness fail-safe | maintenance | small | low | document | open |
| tasks/wash-guides-content-026.json | Hygiene in outbreaks/displacement (household-level cholera prevention) | writing | medium | **high** | document | open |
| tasks/wash-guides-content-027.json | Safe water for the immunocompromised (household practice) | writing | small | **high** | document | open |
| tasks/wash-guides-design-028.json | Low-literacy pictogram set (openly-licensed or original) | design-spec | medium | low | document | open |
| tasks/wash-guides-l10n-029.json | Additional priority languages (low-resource focus) | writing | large | medium | translation | open |
| tasks/wash-guides-content-030.json | School-WASH hygiene-promotion pack | writing | medium | medium | document | open |
| tasks/wash-guides-ops-031.json | Annual re-validation against updated WHO/UNICEF/CDC guidance | maintenance | medium | medium | document | open |
| tasks/wash-guides-sec-032.json | Dependency/supply-chain audit + SRI hardening | maintenance | small | low | pr | open |
| tasks/wash-guides-content-033.json | Read-aloud/audio versions for non-readers | writing | medium | low | document | open |

**Fan-out dimensions:** none (all dimensions are explicitly enumerated in the TASKS.md backlog rows; no
fabrication). **Seed kept:** tasks/wash-guides-arch-001.json.

---

## Example task JSON

Complete, schema-valid Task JSON for the first M0 task. `verifiedNeed` is `false` and `requestor` is
`"TBD"` because **no partner org is secured yet** (honest default per the plan).

```json
{
  "id": "wash-guides-arch-001",
  "title": "ADR: content format (JSON vs MDX) — decide first",
  "project": "wash-guides",
  "type": "design-spec",
  "lane": "donated",
  "priority": "high",
  "domain": ["public-health", "wash", "content", "tooling"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "small",
  "status": "open",
  "context": "wash-guides publishes open, multilingual WASH how-tos that paraphrase and cite authoritative guidance (WHO/UNICEF/CDC/Sphere). The content-unit schema and the static renderer both depend on the storage format, so this ADR is decided first; the schema is provisional until it lands. Content is the primary deliverable and tooling is deliberately light.",
  "objective": "Record an Architecture Decision Record selecting the content format (JSON vs MDX) for WASH content units, weighing structured validation, citation/numeric-claim capture, plain-language authoring ergonomics, translation/i18n, and static rendering, so the schema and renderer can build on a settled foundation.",
  "acceptanceCriteria": [
    "ADR compares JSON vs MDX against criteria: schema/field validation (incl. sources, numericClaims, risk class, review/sign-off fields), authoring ergonomics for plain-language steps, i18n/translation workflow, and static rendering to accessible + printable output",
    "ADR records a decision with rationale and explicitly notes the content schema (data-003) is provisional until this ADR is merged",
    "ADR notes how citations, per-claim numeric values, and review/sign-off metadata are represented in the chosen format",
    "ADR is committed to the repo and referenced by the schema and renderer tasks"
  ],
  "resources": [
    "C:\\code\\elyos\\planning\\projects\\wash-guides\\PLAN.md",
    "C:\\code\\elyos\\packages\\schema\\src\\schemas.ts",
    "C:\\code\\elyos\\docs\\good-deed-definition.md"
  ],
  "output": "A committed ADR document selecting the WASH content format (JSON vs MDX) with rationale, consumed by the content-schema and renderer tasks.",
  "requestor": "TBD",
  "verifiedNeed": false,
  "outputLicense": "CC-BY-4.0"
}
```
