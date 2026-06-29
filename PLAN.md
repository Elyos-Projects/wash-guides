# PLAN — wash-guides (open water, sanitation & hygiene how-tos)

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## Executive summary

**wash-guides** is an open, multilingual, freely-reusable body of practical **water, sanitation and
hygiene (WASH)** how-tos — handwashing, household water treatment and safe storage, safe sanitation
and excreta disposal, menstrual health and hygiene, household cleaning/disinfection, and hygiene in
outbreak/displacement settings. Each how-to is a small, structured content unit that **paraphrases
and cites authoritative public-health guidance** (primarily WHO and UNICEF, plus CDC and sector
references such as the Sphere Handbook) and is review-gated for accuracy before it ships. The output
is plain-language, low-literacy-friendly, and printable for last-mile distribution where connectivity
is poor — which is precisely where WASH need is highest.

The work has two coupled lanes: (1) **content** — per-topic × language WASH units, each
source-cited, accuracy-reviewed, and (for any clinical or chemical-dosing topic) signed off by a
credentialed expert; and (2) **light tooling** — a content schema, validation/CI, and a static,
offline-friendly renderer that emits printable, attributed how-tos. The tone is calm, practical, and
dignity-preserving; this is a public good, never a commercial or fear-driven product.

This is a **medium risk-tier** project **with an embedded HIGH-risk sub-class.** Most hygiene and
sanitation how-tos are medium risk (domain-accuracy review required). But a defined sub-set crosses
into safety/medical territory where a wrong number or instruction can directly harm a person — most
critically **oral rehydration solution (ORS) preparation and dehydration danger-signs** (clinical)
and **chemical water-treatment dosing** (e.g., household chlorination concentrations, contact times).
These are treated as **HIGH risk** and **must not ship without credentialed-expert sign-off**, an
independent **numeric/dosing verification** step, and a persistent **"informational, not a substitute
for professional medical care or trained WASH practice"** disclaimer. A hard scope guardrail bars
genuinely clinical instruction (e.g., diagnosing or treating disease, IV rehydration, medication
dosing) — we link to qualified sources and care rather than improvise.

**Honesty note on the partner.** No partner organization, requestor, or field deployment has been
secured. There is strong, well-documented general need for accessible, accurate, openly-licensed WASH
information, so foundation and content work can proceed as a generic public good — but **partner,
requestor, verified-need, and the credentialed-expert reviewer are all `TO BE SECURED`** and tracked
with dated outreach and an explicit build-vs-hold decision rule (see *Problem & beneficiaries*,
*Quality, review & risk gates*, and *Open questions*). HIGH-risk content does **not** begin until a
credentialed expert reviewer is secured.

## Problem & beneficiaries

**The problem.** Unsafe water, inadequate sanitation, and poor hygiene remain among the largest
preventable causes of illness and death worldwide, concentrated in low-resource and crisis-affected
communities. Authoritative, *correct* guidance exists (WHO, UNICEF, CDC, the Sphere standards) but is
fragmented across long PDFs and institutional websites, frequently English-only, written above the
literacy level of the people who most need it, and copyright-restricted in ways that block direct
reuse. At the moment a household needs to make safe drinking water, build/maintain a latrine, or
respond to a child's diarrhea, that guidance is hard to find, hard to read, hard to act on, and often
unavailable offline. The gap is filled by inconsistent, unsourced, sometimes dangerous folk advice.

**Who is helped (beneficiaries).**
- **Households and individuals** in low-resource, rural, peri-urban, and crisis/displacement settings
  who need to make water safe, manage sanitation safely, and practice protective hygiene — especially
  caregivers of young children, pregnant people, people managing menstruation, and people with low
  literacy or limited access to the dominant language.
- **Frontline last-mile actors** — community health workers, WASH NGOs, school and clinic hygiene
  promoters, and mutual-aid/relief groups — who need free, accurate, brandable, printable,
  translatable materials instead of building their own or distributing copyrighted PDFs.
- **Translators and educators** who can build on an openly-licensed, well-sourced base.

**Verified need / partner / requestor: TO BE SECURED.** No NGO, ministry, health agency, or community
organization has yet confirmed this specific need in writing or agreed to adopt the output, and no
credentialed expert reviewer is yet engaged. The *general* need is strongly evidenced by the public
health record regardless of any single partner, so M0–M1 (foundation + medium-risk content) proceed
as a generic public good. **HIGH-risk content (M2) is hard-gated on a secured credentialed expert.**
Partner-facing delivery (field validation, adoption) is gated on a secured partner. Outreach is
**dated, not open-ended**: credentialed WASH/clinical expert reviewer engaged by **2026-09-30** (M2
entry gate); ≥ 2 candidate distribution partners (WASH NGO, ministry of health WASH unit, community
health network, or school-health program) in active conversation by **2026-10-31**; a named
adopting/distributing partner + steward by **2026-12-31** (delivery gate). **Decision rule:** if no
credentialed expert is secured by the M2 entry date, HIGH-risk content does **not** start and the
project holds at M1 (medium-risk content only); if no partner is secured by **~2027-03-31**, the
steward + Elyos governance declare **"Publicly Shipped (generic public good)"** rather than shipping
to no one, with outreach continuing so a later adoption upgrades the status.

## Goals and non-goals

**Goals.**
- Publish accurate, **source-cited, paraphrased** WASH how-tos covering the core protective behaviors,
  each traceable to named authoritative guidance and passing accuracy review before it ships.
- Make the content **plain-language and low-literacy-friendly** (short steps, controlled vocabulary,
  visual/pictographic support), and **printable offline** for last-mile distribution.
- Treat the safety/medical sub-set (ORS/dehydration, chemical water-treatment dosing) as **HIGH risk**:
  credentialed-expert sign-off + independent numeric verification + "not a substitute for professional
  care/training" framing before any such unit ships.
- Be genuinely **open and reusable**: MIT tooling, **CC-BY-4.0** original content — produced by
  paraphrasing facts and citing sources, **never** by copying copyrighted text or reproducing logos.
- Support **internationalization** with safety-accuracy-reviewed translations, prioritizing
  low-resource languages where WASH need is greatest.
- Be **adoptable** by a frontline WASH/health partner in their community's languages and context.

**Non-goals.**
- **Not medical/clinical instruction.** Not diagnosis, not treatment protocols, not medication or IV
  dosing, not a substitute for a clinician. We cover *prevention and safe household practice* and link
  out for care.
- Not engineering design specs for large/community water or sanitation infrastructure (e.g., treatment
  plant design, borehole drilling, sewer engineering) — household and small-community practice only.
- Not original research, field measurement, or endorsement of any specific commercial product/brand
  (water filters, chlorine products, etc.) — we describe generic methods and cite authorities.
- Not a data-collection product: no accounts, no analytics, no telemetry, no person-level data.
- Not a real-time outbreak alerting or surveillance system.
- Not content in any language we cannot source-verify and safety-review.

## Success metrics (outcomes)

Outcome-centric and beneficiary-first; vanity metrics (page views, stars, downloads alone) are
explicitly **not** success. Baselines are zero at project start unless noted.

| Outcome | Baseline | Target (first 12 months post-launch) | How measured (privacy-preserving) |
| --- | --- | --- | --- |
| Core WASH how-tos shipped & accuracy-reviewed | 0 | ≥ 12 medium-risk topics, each source-cited and signed off | In-repo review log |
| HIGH-risk units with credentialed-expert sign-off | 0 | 100% of shipped ORS/dehydration & dosing units carry recorded expert sign-off + numeric verification | Governance/review log |
| Dosing/numeric accuracy | n/a | 0 shipped numeric instruction (dose, ratio, contact time) without independent second-checker + expert confirmation | Numeric-verification log; CI numeric-citation check |
| Source-citation coverage | n/a | 100% of claims carry a named authoritative citation with retrieval date + license note | Citation-coverage test in CI |
| Languages with safety-reviewed content | 1 (en) | ≥ 3 languages, each translation safety-accuracy reviewed | Translation completeness + review log |
| Readability / accessibility | none | Plain-language target met (e.g., short steps, controlled vocabulary); WCAG 2.2 AA for any rendered site; printable offline | Readability check + axe/manual a11y audit |
| Provenance/license integrity | n/a | 0 units with verbatim copied source text or reproduced third-party logo/emblem | Provenance audit + similarity/copy check in CI |
| Partner adoption | 0 | ≥ 1 named WASH/health partner adopts/distributes; outreach to ≥ 2 | Signed letter of support / MOU (manual record) |
| Last-mile reach (partner-reported, opt-in) | 0 | ≥ 3,000 distinct people/households reached, partner-attested | Partner self-report template (no in-app tracking) |
| Privacy posture | n/a | 0 telemetry endpoints, 0 trackers, 0 PII fields | Static + runtime audit on any rendered site |

**Reach measurement — windows, denominators, anti-double-counting.** "Reach" counts **distinct
people/households** (not page views, downloads, or leaflets printed) over a **rolling 12-month window**
from launch; each partner counts a recipient **once per reporting period** across touchpoints; reach
by multiple partners is **de-duplicated at roll-up** (best-effort, partner-attested, overlap noted);
estimates are recorded **as estimates**, separate from confirmed counts. Because we collect no
telemetry, reach is partner self-report — an honest privacy/measurement trade-off.

## Scope

**In scope.**
- Structured WASH how-to content units across: **handwashing** (technique + critical times);
  **household water treatment & safe storage (HWTS)** — boiling, household chlorination, solar
  disinfection (SODIS), filtration, settling/flocculation; **safe water storage**; **safe sanitation
  & excreta disposal** (latrine use/maintenance, safe disposal of child feces); **menstrual health &
  hygiene (MHH)**; **household cleaning & surface disinfection**; **hygiene in emergencies/outbreaks**
  (e.g., cholera-prevention behaviors at the household level).
- The **HIGH-risk sub-set**, gated and clearly framed: **ORS preparation and dehydration danger-signs
  (when to seek care)** and **chemical water-treatment dosing** (chlorine concentrations, contact
  times, SODIS conditions).
- A content schema (topic, risk-class, language, sources, review/sign-off status, numeric-verification
  record), validation tooling, and CI gates.
- A plain-language style guide + controlled vocabulary; optional openly-licensed/original pictograms.
- A static, offline-friendly renderer producing printable, attributed how-tos; i18n with safe locale
  fallback.
- Provenance + review log for every unit; per-source license verification.

**Out of scope (explicit).**
- Clinical diagnosis/treatment, medication/IV dosing, or any instruction that substitutes for a
  clinician or trained WASH technician (link out only).
- Large/community water & sanitation **engineering design** (treatment plants, piped networks,
  borehole/well drilling, sewerage) — household/small-community practice only.
- Product/brand recommendations, reviews, or affiliate content; commercial use steering.
- Accounts, analytics, telemetry, advertising, or any person-level data collection.
- Content in unverifiable/unreviewable languages; verbatim reuse of copyrighted text/logos.
- Real-time alerting, surveillance, mapping of individuals, or outbreak reporting.

## Solution approach & architecture

**Overview.** A content-first pipeline. The primary deliverables are **structured, source-cited
content units** (documents/datasets); supporting code is intentionally light — a schema, a validator,
CI gates, and a static renderer. No backend and no runtime data collection are required.

**Pipeline / components.**
- **Content units (the core asset):** small, structured how-tos keyed by `(topicId, lang)`, authored
  by paraphrasing authoritative guidance and citing it. Each unit declares its **risk class**
  (`medium` or `high`) which drives the required review gates.
- **Content schema + validator:** enforces required fields (sources with license, risk class, review
  status, separate author vs. approver, numeric-verification record for any dosing/numeric claim) at
  build time; a unit missing a required field, citing an unverified-license source, self-approved, or
  carrying an unverified numeric value **fails validation**.
- **Style/readability layer:** a plain-language style guide + controlled vocabulary; a readability
  check in CI flags units that exceed the target reading level or step length.
- **Renderer (static, offline-friendly):** emits accessible HTML + **print-optimized** output
  (print CSS / client-side PDF), with attribution and the risk-appropriate disclaimer baked in. No
  server, no telemetry, CSP `connect-src 'none'`.
- **i18n layer:** locale catalogs + per-unit translations with safe fallback to a verified language;
  translations are safety-accuracy reviewed, not merely fluent; bundled offline fonts/glyph coverage
  for shipped scripts; RTL support where a target language needs it.
- **Provenance + review log:** PR-tied, append-only entries binding each approval to a commit (sources
  checked, reviewer + distinct approver, numeric verification, divergence decisions).

**Tech stack.** TypeScript, ESM, pnpm workspaces. Content as structured files (JSON/MDX — format
decided by ADR in M0). Static site generation; testing via Vitest (schema/validation), axe-core/pa11y
+ manual audit (a11y), Playwright (offline/print + no-egress). License: **MIT** (tooling) /
**CC-BY-4.0** (content).

**Data model (content unit).**
```
WashUnit {
  id: string                  // e.g. "handwashing-technique"
  topic: string               // e.g. "handwashing" | "hwts-chlorination" | "ors"
  riskClass: "medium" | "high"
  title: localized string
  audience: string[]          // e.g. ["household","caregiver","chw"]
  steps: localized step[]      // short, plain-language, sequential
  numericClaims: NumericClaim[]   // { value, unit, context, sourceRef, verifiedBy, expertConfirmed }
  sources: Citation[]          // { org, title, url, retrievedDate, sourceLicense, licenseVerified }
  reviewStatus: "draft" | "in-review" | "approved"
  reviewedBy: string           // author / domain reviewer
  approvedBy: string           // MUST differ from reviewedBy (no self-approval)
  expertSignOff?: ExpertSignOff // REQUIRED when riskClass = "high"
  reviewLogRef: string         // PR-tied, append-only review-log entry
  disclaimer: string           // risk-appropriate; "informational, not a substitute…" for high
  lang: string
  contentLicense: "CC-BY-4.0"
  contentVersion: string
  lastReviewed: date
  validUntil: date             // drives staleness fail-safe
}
NumericClaim { value; unit; context; sourceRef; verifiedBy; expertConfirmed }  // dosing/ratios/times
ExpertSignOff { name; credential; scope(version+citations); date; consentToCredit }
```

**Key decisions (ADRs, M0).**
1. **Content format** (JSON vs. MDX) — decided **first**; the schema and renderer depend on it (the
   schema is provisional until this ADR lands).
2. **Risk-classification policy** — the explicit, documented rule for which topics are `high`
   (clinical or chemical-dosing) vs `medium`, and the gates each triggers.
3. Renderer/static-site tooling, print/PDF approach, and the no-egress posture.
4. i18n approach (catalogs, fallback, RTL, offline fonts) — settled as input to renderer choice.
5. Numeric-verification mechanism (how dosing values are second-checked and CI-enforced).

## Data, licensing & compliance

**This section is load-bearing. Be conservative.** WASH guidance comes from institutions whose
copyright terms are **restrictive**, and getting this wrong is both a legal and an ethical failure.

**Content sources (authoritative).** WHO (e.g., guidelines on drinking-water quality, sanitation,
hand hygiene, HWTS), UNICEF (WASH programming and hygiene-promotion materials), CDC (handwashing,
household water treatment, healthy water), and sector references such as the **Sphere Handbook** (WASH
minimum standards) and the IFRC/WASH cluster materials. Each unit cites its sources with org, title,
URL, retrieval date, and the source's **license/terms**.

**Licensing rigor (critical — read carefully).**
- **Our outputs:** tooling under **MIT**; content under **CC-BY-4.0**.
- **WHO content is typically licensed `CC BY-NC-SA 3.0 IGO`** — i.e., **non-commercial** and
  **share-alike**. This is *incompatible* with our CC-BY-4.0 output and with downstream commercial/
  unrestricted reuse. We therefore **do not copy or adapt WHO text** and **do not relicense it**.
  Instead we **paraphrase the underlying facts** (facts and methods are not copyrightable; only their
  expression is) and **cite** the source. Direct quotation, if ever unavoidable, is minimal, clearly
  attributed, and kept under fair-use/fair-dealing — but the default is **paraphrase + cite, never
  copy**.
- **UNICEF and IFRC content is copyrighted**; **CDC** materials are largely U.S. Government works
  (generally public domain) but may embed third-party copyrighted figures — verify per asset. The
  **Sphere Handbook** is freely available but copyrighted; cite, don't copy.
- **Logos/emblems are off-limits.** The **WHO and UN/UNICEF emblems are specially protected** (the WHO
  emblem under World Health Assembly regulations; UN emblems under international rules) and must
  **never** be reproduced. Reproducing them could also falsely imply endorsement. We use **no**
  third-party logos, emblems, or trademarks.
- **No implied endorsement.** Citing a source is not endorsement by that source. Every rendered output
  states that the material is *derived from and cites* authoritative guidance but is **not an official
  WHO/UNICEF/CDC product** and is **not endorsed** by them unless an explicit endorsement exists.
- **Per-source verification before ship:** each source's reuse terms are checked and recorded
  (`sourceLicense`, `licenseVerified`) before any unit citing it ships. Where terms are unclear or
  restrictive, we link rather than embed, and paraphrase only.

**Source-divergence precedence.** Where authorities differ on a safe action: (1) for health/clinical
guidance prefer **WHO**, harmonized with local ministry-of-health guidance where a target region is
known; (2) for U.S.-context practice, **CDC**; (3) for humanitarian/emergency settings, **Sphere /
WASH cluster**; (4) where credible sources **materially disagree on a safety-critical instruction
(especially a dose or contact time), state the divergence and link both rather than averaging** — and
record the decision in the review log. Numeric values are always tied to a specific cited source.

**Provenance model.** Every unit carries `sources[]` (with retrieval dates + verified license),
`numericClaims[]` (each tied to a source and a verifier), and a PR-tied review-log entry. A repo-level
provenance/review log is the auditable record the *Definition of Shipped* checks against.

**Privacy / PII stance.** **Zero person-level data.** WASH how-tos are general public content; we
collect, store, and publish **no PII** — no accounts, analytics, telemetry, cookies (beyond what a
static offline renderer strictly needs), or third-party scripts. No real people, case histories, or
identifiable images are used. Any illustrative imagery is original or openly-licensed and depicts no
identifiable individual without documented consent (default: avoid identifiable people entirely).

**Cultural & dignity review.** Sanitation and menstrual-health content is reviewed for cultural
appropriateness, gender sensitivity, and dignity — guidance that is technically correct but culturally
inapt or stigmatizing is treated as not yet shippable.

## Quality, review & risk gates

**Risk tier: medium overall, with a HIGH-risk sub-class** (clinical: ORS/dehydration; chemical-dosing:
water-treatment concentrations/contact times). Per `docs/good-deed-definition.md`, HIGH-risk
health/safety content **requires credentialed-expert sign-off before merge**.

**Required reviews before a deed is "done":**
- **Tooling/renderer (low–medium):** maintainer code review + CI green (lint, typecheck, unit, a11y,
  offline/print E2E, no-egress audit).
- **Medium-risk content:** a reviewer with WASH/public-health domain knowledge verifies every claim
  against the cited authoritative sources; the **scope guardrail** is enforced (no clinical/medical
  instruction; link out). **No self-approval:** `reviewedBy` (author) and `approvedBy` must be distinct
  people. A PR-tied review-log entry is written.
- **HIGH-risk content (hard gate — no expert, no ship):**
  - **Credentialed-expert sign-off** is mandatory. Credential bar: a **WASH / environmental-health
    professional** (e.g., MPH in environmental health, registered sanitarian/REHS, or equivalent
    field-recognized WASH qualification) for water-treatment/dosing content; and a **licensed clinician**
    (physician/nurse) for ORS/dehydration danger-sign content. Sign-off is **version-scoped** (attaches
    to a specific content version + citation/numeric set; edits require re-sign-off) and recorded with
    name, credential, and consent in a reviewers ledger.
  - **Independent numeric verification:** every dose, ratio, concentration, and contact time is
    **second-checked by a person other than the author** against the cited source, recorded in
    `numericClaims[].verifiedBy`, and **confirmed by the credentialed expert** (`expertConfirmed`). CI
    fails any HIGH unit with an unverified numeric claim.
  - **"Informational, not a substitute" framing:** every HIGH unit renders a persistent disclaimer —
    *"This is general information, not a substitute for professional medical care or trained WASH
    practice; seek qualified help for serious symptoms or uncertainty"* — plus explicit **danger-signs /
    when-to-seek-care** content where relevant (e.g., signs of severe dehydration).
- **Translations:** reviewed by a competent speaker **and** re-checked for **safety accuracy** (numbers,
  doses, danger-signs, step order), not just fluency. HIGH-risk translations require the same numeric
  verification and, where feasible, expert spot-check in the target language.
- **Cultural/dignity review** for sanitation and menstrual-health units (see *Data, licensing &
  compliance*).
- **Accessibility:** any rendered site meets **WCAG 2.2 AA** (automated + manual AT audit); printable
  output is legible and low-literacy-friendly.

**Staleness is fail-safe.** Each source/unit carries `lastReviewed` + `validUntil` (per-topic review
interval). Past `validUntil`, a unit is auto-flagged ("verify before relying") and, for HIGH-risk
units, **withheld** until re-verified and re-signed-off — so corrected guidance can never be served
silently stale.

**Definition of Shipped (project-level).** A published set of WASH how-tos that: (1) are
source-cited, accuracy-reviewed, and within scope; (2) carry **credentialed-expert sign-off + numeric
verification + "not a substitute" framing for every HIGH-risk unit**; (3) respect all source licenses
(no copied text, no reproduced logos/emblems) with recorded provenance; (4) are plain-language,
accessible, and printable offline; (5) collect no telemetry/PII; and (6) are **adopted/distributed by
a named WASH/health partner in that community's language(s)**. Until a partner is secured, criteria
(1)–(5) define **"Publicly Shipped (generic public good)"**; criterion (6) upgrades to
"partner-adopted." HIGH-risk units cannot be part of *any* shipped state without (2).

## Roadmap & milestones

Phased; each phase has measurable exit criteria. M0 is a thin cold-start; the HIGH-risk phase (M2) is
hard-gated on a secured credentialed expert; partner-facing delivery (M4) is gated on a secured partner.

- **M0 — Foundation & cold-start (thin slice).**
  *Goal:* the content schema, risk-classification policy, provenance/review-log format, CI gates, plain-
  language style guide, and **one medium-risk sample unit** exist.
  *Exit:* **content-format ADR decided first**, then schema + provenance/review-log finalized;
  **risk-classification policy ADR** recorded (which topics are HIGH and the gates they trigger);
  CI runs schema validation, citation-coverage, no-self-approval, readability, and (for any rendered
  output) a11y + no-egress checks; **one medium-risk unit (handwashing technique)** authored, fully
  source-cited, paraphrased (no copied text/logos), and domain-reviewed by an approver distinct from
  the author. **No HIGH-risk content in M0.**

- **M1 — Core medium-risk content + renderer.**
  *Goal:* the bulk of protective-behavior how-tos (medium risk) + the static, printable, accessible
  renderer.
  *Exit:* ≥ 8 medium-risk topics authored, source-cited, and reviewed (handwashing, safe water storage,
  boiling, SODIS, filtration, latrine use/maintenance, safe disposal of child feces, household surface
  disinfection); renderer emits accessible HTML + printable output offline with attribution +
  disclaimer; WCAG 2.2 AA pass (automated + manual); no-egress verified; provenance/license audit green.

- **M2 — HIGH-risk content (expert-gated).**
  *Goal:* the safety/medical sub-set, behind the full HIGH-risk gate.
  *Exit (gated on a secured credentialed expert):* ORS preparation + dehydration danger-signs (clinician
  sign-off) and chemical water-treatment dosing/contact-time units (WASH/EH expert sign-off) shipped
  with **independent numeric verification**, **"informational, not a substitute" framing**, and
  danger-sign/when-to-seek-care content; CI numeric-verification gate green; scope guardrail enforced
  (no clinical treatment instruction). *If no expert is secured by 2026-09-30, M2 does not start and the
  project holds at M1.*

- **M3 — i18n & localization.**
  *Goal:* internationalization + ≥ 2 non-English locales, safety-accuracy reviewed.
  *Exit:* i18n framework with build-time completeness + safe fallback; ≥ 2 priority-language locales for
  the core medium-risk set and any shipped HIGH-risk units; translations safety-accuracy reviewed
  (numbers/doses/danger-signs/step order), with numeric verification re-run per language; RTL exercised
  if a target language needs it.

- **M4 — Partner adoption & field validation (the deed).**
  *Goal:* a real frontline partner adopts/distributes the material and it reaches beneficiaries.
  *Exit (Definition of Shipped, partner-adopted):* a named WASH/health partner endorses/distributes the
  content in their community's language(s); field-appropriateness confirmed; outcomes-tracking process
  (partner self-report) in place. *Gated on a secured partner — TO BE SECURED.*

Dependencies: M1 → M0 (schema + renderer); **M2 → secured credentialed expert** (and M0/M1 base);
M3 → M1/M2 (stable content to localize); M4 → M3 (multilingual base) + **secured partner** (can start
in parallel). The **risk-classification policy (M0) gates which units enter M2.**

## Work breakdown

The itemized, schema-mapped backlog lives in **TASKS.md**, organized by the M0–M4 milestones above.
Each task maps to an Elyos Task JSON (per `packages/schema/src/schemas.ts`), is sized, risk-tagged, and
names a reviewer. TASKS.md also includes acceptance criteria for the most important tasks per
milestone, milestone Definitions of Done, a backlog, and a complete, schema-valid example Task JSON
(with `verifiedNeed: false` because no partner is yet secured). The first build item is the
content-format ADR, immediately followed by the risk-classification policy and content schema,
reflecting that risk-class drives every downstream gate.

## Governance, roles & stakeholders

- **Maintainer (Owner): TBD.** Owns the repo, schema, CI, roadmap, releases, and review standards.
- **Code reviewers:** rotation of TS-competent contributors; ≥ 1 approval + CI green to merge.
- **WASH/public-health content reviewers:** contributors with domain knowledge; verify medium-risk
  claims against cited sources; enforce the scope guardrail.
- **Credentialed expert reviewers (HIGH tier): TO BE SECURED** — a WASH/environmental-health
  professional (dosing/water-treatment) and a licensed clinician (ORS/dehydration). Version-scoped
  sign-off, recorded with credential + consent in a reviewers ledger; **veto** on whether HIGH-risk
  content is safe to ship (a maintainer cannot override a "do not ship" on substance; disagreement is
  logged and escalated to Elyos governance / a second expert).
- **Numeric verifier:** a second person (not the author) who independently re-checks every dose/ratio/
  contact-time against the source before expert confirmation.
- **Translation reviewers:** competent speakers per locale, paired with a safety-accuracy re-check
  (and numeric re-verification for HIGH units).
- **Cultural/dignity reviewer:** for sanitation and menstrual-health content.
- **Accessibility reviewer:** competent with assistive tech; manual AT audits of any rendered site.
- **Steward (last-mile owner): TO BE SECURED** — owns distribution, the partner relationship, and
  getting the material into beneficiaries' hands.
- **Partner / requestor: TO BE SECURED** — a named WASH/health org confirming need, priority topics,
  and languages, and ultimately adopting/distributing.
- **Elyos governance/board:** arbitrates edge cases, risk-tier calls, and license decisions.

## Dependencies & integrations

- **External content sources:** WHO, UNICEF, CDC, Sphere Handbook, IFRC/WASH cluster (read-only
  references; **license-checked per use**; paraphrase + cite only).
- **Human/expert dependencies (critical path):** a secured **credentialed expert reviewer** (blocks M2
  HIGH-risk content) and a secured **partner/steward** (blocks M4 delivery). These are the gating
  non-software dependencies.
- **Tooling/libraries:** content schema + validator, static-site/renderer tooling, i18n library, test
  stack (Vitest, Playwright, axe-core/pa11y), client print/PDF; offline fonts.
- **Hosting:** static host (GitHub Pages / Netlify / Cloudflare Pages) — no app server, no backend.
- **Elyos pieces:** Task schema (`packages/schema`), CLI workspace prep / PR flow (donated lane),
  good-deed definition & risk-tier governance, review/sign-off process.

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |
| Inaccurate WASH guidance causes illness/harm | Medium | High | Mandatory source-cited accuracy review per unit; WASH-domain reviewer; scope guardrail (no clinical instruction; link out) | Content reviewer |
| **Wrong dose/ratio/contact time** (ORS, chlorination) directly harms a person | Medium | **Critical** | HIGH-risk class; independent numeric second-check + credentialed-expert confirmation; CI numeric-verification gate; cite exact source per value; state divergence rather than average | Expert / Numeric verifier |
| Copyright/license breach — copying WHO/UNICEF text or relicensing CC BY-NC-SA content as CC-BY | Medium | High | Paraphrase facts + cite, never copy or adapt; verify each source license before ship; default "link, don't embed"; provenance log; copy/similarity check in CI | Maintainer |
| Reproducing WHO/UN/UNICEF emblems or implying endorsement | Medium | High | No third-party logos/emblems ever; explicit "not an official/endorsed product" notice on every output | Maintainer |
| HIGH-risk content shipped without expert (gate bypass) | Low | Critical | Hard CI/governance gate: `riskClass:high` requires recorded `expertSignOff`; build fails otherwise; no expert ⇒ hold at M1 | Maintainer / Expert |
| No credentialed expert secured → M2 blocked | Medium | High | Dated outreach (expert by 2026-09-30) via public-health/WASH networks, MPH programs, sanitarian associations; hold at M1 rather than ship unreviewed | Steward / Maintainer |
| No partner secured → cannot reach partner-adopted shipped | Medium | High | Honest `TO BE SECURED`/`verifiedNeed:false`; dated outreach; **"Publicly Shipped (generic public good)"** decision at ~2027-03-31 so finished content isn't stranded; later adoption upgrades status | Steward |
| Translation introduces safety errors (doses/danger-signs) | Medium | High | Translations safety-accuracy reviewed + numeric re-verified per language; competent speaker + safety reviewer pair; expert spot-check for HIGH units | Translation reviewer |
| Content goes stale vs. updated official guidance | High | Medium | `lastReviewed`/`validUntil` fail-safe (auto-flag; withhold HIGH units past window); periodic re-review cadence; maintenance tasks | Content reviewer |
| Cultural insensitivity / stigma (sanitation, MHH) | Medium | Medium | Cultural/dignity review gate; partner/community input where available | Cultural reviewer |
| Misuse: hostile fork implying official endorsement | Low | Medium | Clear license + "not official/endorsed" disclaimer; attribution terms; no emblems to misuse | Maintainer |
| Maintainer bandwidth / bus factor | Medium | Medium | Reviewer rotation; documented processes; MIT/CC-BY low lock-in | Maintainer |

## Security & privacy

**Threat surface.** Small: a static, no-backend, no-PII content project. Principal concerns: (1)
**content-integrity** — a wrong or maliciously edited dose/instruction is the highest-impact failure;
(2) supply-chain risk in build dependencies; (3) third-party script/tracker creep in any rendered
site; (4) hostile forks implying official endorsement; (5) license/provenance breach.

**Controls.**
- **No secrets** in code/logs/receipts (Elyos rule); static hosting only; nothing to leak.
- **No telemetry / no PII:** strict CSP with `connect-src 'none'`; a runtime no-egress E2E that fails
  the build on any unexpected outbound request; static audit for trackers/PII fields. No accounts, no
  analytics, no person-level data anywhere.
- **Content-integrity controls (top priority):** every claim source-cited and review-gated; **every
  numeric value independently second-checked + expert-confirmed**; PR-tied, append-only review log
  binds approvals to commits; CI blocks merges of HIGH units lacking `expertSignOff` or with unverified
  numerics; `validUntil` staleness fail-safe withholds expired HIGH content.
- **Supply chain:** pinned/locked deps (pnpm lockfile), dependency review, minimal deps, CI dependency
  audit, SRI where applicable.
- **Provenance/license integrity:** per-source license verification recorded before ship; copy/
  similarity check guards against verbatim reuse; no third-party logos/emblems.
- **Abuse/misuse prevention:** prominent "not an official/endorsed WHO/UNICEF/CDC product" notice;
  attribution/branding terms documented; scope guardrail prevents repurposing into clinical advice.

## Sustainability & maintenance

- **Ownership after delivery:** the **maintainer** owns content/tooling/releases; the **steward** owns
  distribution and the partner relationship. Both are **TBD** and must be named before M4.
- **Content freshness:** units carry `lastReviewed`/`validUntil`; a **periodic re-review cadence**
  (recommended at least annually and after any change to official guidance, shorter for HIGH-risk
  dosing/clinical units) is enforced via maintenance tasks and the runtime staleness fail-safe; HIGH
  units past their window are withheld until re-verified and re-signed-off.
- **Outcomes tracking:** no telemetry, so adoption/reach is tracked via **partner self-report** and a
  manual record of endorsements/MOUs — an explicit privacy/measurement trade-off.
- **Low lock-in:** MIT/CC-BY, static hosting, standard formats keep the project forkable and cheap to
  run, improving long-term survivability and translation by others.

## Open questions

1. **Credentialed expert reviewer:** Who signs off HIGH-risk (clinical ORS/dehydration + WASH dosing)
   content? Hard gate for M2; **outreach deadline 2026-09-30.** Needs a human decision.
2. **Partner / requestor:** Which WASH/health org confirms need, priority topics, and languages, and
   adopts/distributes? `TO BE SECURED`; outreach by 2026-10-31, partner by 2026-12-31.
3. **Priority topics & context:** Which topics first (should be partner/context-driven once secured)?
   Provisional M1 set listed in the roadmap.
4. **Priority languages:** First non-English locales should be low-resource languages where WASH need
   is greatest — partner-driven once secured (provisional choice recorded at M3).
5. **Content format & renderer:** final ADR decisions (M0).
6. **Sphere / source reuse:** confirm the paraphrase/citation stance and per-source license notes; do
   we need a one-time check of the CC BY-NC-SA-IGO non-relicensing stance for WHO-derived facts?
7. **Pictograms:** source openly-licensed sets or commission original low-literacy pictograms? (License
   must be clean.)
8. **HIGH-risk scope line:** confirm with the expert exactly where "safe household practice" ends and
   "clinical instruction" (out of scope) begins for borderline topics (e.g., ORS for an infant).

## References

- Elyos work rules & refusal guardrails — `C:\code\elyos\CLAUDE.md`
- Good-deed definition & risk tiers — `C:\code\elyos\docs\good-deed-definition.md`
- Task JSON schema — `C:\code\elyos\packages\schema\src\schemas.ts`
- Portfolio roadmap (wash-guides entry, Track 6) — `C:\code\elyos\planning\ROADMAP.md`
- Sibling Elyos plans for house style — `planning/projects/proper-prepper/{PLAN,TASKS}.md`,
  `planning/projects/public-official-guide/{PLAN,TASKS}.md`
- Authoritative content sources (license-checked per use; paraphrase + cite only): WHO (drinking-water
  quality, sanitation, hand hygiene, HWTS guidance), UNICEF (WASH/hygiene promotion), CDC (handwashing,
  household water treatment, healthy water), Sphere Handbook (WASH minimum standards), IFRC/WASH cluster.
- Licensing notes: WHO publications commonly `CC BY-NC-SA 3.0 IGO` (non-commercial, share-alike — not
  relicensable; paraphrase facts + cite); WHO emblem protected under WHA regulations; UN/UNICEF emblems
  protected — never reproduce.
- WCAG 2.2 AA (W3C Web Content Accessibility Guidelines).

---

## Appendix A — Improvements applied

The following 25 specific improvements were identified against the first draft and **applied** in the
text above (not merely proposed). Each notes what changed and where.

1. **Split the risk tier into medium + an explicit HIGH sub-class.** Rather than calling the whole
   project "medium," the executive summary, *Quality gates*, and the schema (`riskClass`) name a HIGH
   sub-set (ORS/dehydration, chemical dosing) so the strongest gate attaches only where harm is real.
2. **Added an independent numeric-verification gate.** Every dose/ratio/contact time is second-checked
   by a non-author and expert-confirmed (`numericClaims[].verifiedBy`/`expertConfirmed`), with a CI
   gate — added to *Quality gates*, the data model, success metrics, and risks.
3. **Made the WHO `CC BY-NC-SA 3.0 IGO` incompatibility explicit.** *Data, licensing & compliance* now
   states WHO content is non-commercial + share-alike, cannot be relicensed CC-BY, and is handled by
   paraphrasing facts + citing — a real, easily-missed legal trap.
4. **Banned reproduction of WHO/UN/UNICEF emblems specifically.** Added the specially-protected-emblem
   note and a dedicated risk row, beyond a generic "no logos."
5. **Added a "not an official/endorsed product" notice** baked into every rendered output, to prevent
   false implied endorsement by cited authorities.
6. **Hard-gated M2 on a secured credentialed expert** with a dated deadline (2026-09-30) and an
   explicit "hold at M1" rule if unmet — mirroring public-official-guide's discipline.
7. **Defined the credential bar precisely** (WASH/EH professional for dosing; licensed clinician for
   ORS/dehydration) instead of a vague "expert."
8. **Added "informational, not a substitute for professional care/training" framing** as a required,
   persistent disclaimer on every HIGH unit, with when-to-seek-care/danger-sign content.
9. **Added a staleness fail-safe** (`validUntil`) that withholds expired HIGH content until re-signed-off
   — borrowed from public-official-guide — so dosing guidance can't silently go stale.
10. **Added no-self-approval role separation** (`reviewedBy` ≠ `approvedBy`) enforced in CI — borrowed
    from proper-prepper.
11. **Added a cultural/dignity review gate** for sanitation and menstrual-health content, recognizing
    that technically-correct guidance can still be stigmatizing or inapt.
12. **Added a plain-language/readability layer + CI check**, since the beneficiaries are often
    low-literacy and the value collapses if the text is unreadable.
13. **Sequenced the content-format ADR first**, making the schema provisional until it lands (avoids
    rework) — borrowed from proper-prepper's decision-ordering discipline.
14. **Added an explicit risk-classification policy ADR** in M0 so "which topics are HIGH" is a
    documented, auditable decision, not ad hoc.
15. **Narrowed scope away from engineering**: explicitly excluded treatment-plant/borehole/sewer design
    so the project stays in household/small-community practice it can safely cover.
16. **Excluded product/brand recommendations** (filters, chlorine products) to keep it a public good
    and avoid de-facto commercial endorsement.
17. **Made source-divergence precedence safety-aware**: for safety-critical numbers, state divergence
    and link both rather than averaging — added to *Data, licensing & compliance*.
18. **Specified privacy as zero person-level data**, including avoiding identifiable people in imagery,
    not just "no analytics."
19. **Added a copy/similarity check in CI** to actively guard against verbatim reuse of copyrighted
    source text, not just a policy statement.
20. **Reframed success metrics to outcomes** (reviewed units, expert-signed HIGH units, numeric
    accuracy, partner-reported reach) and removed vanity metrics; added de-dup/window rules for reach.
21. **Added the "Publicly Shipped (generic public good)" success state** with a dated decision point so
    finished content isn't stranded if no partner appears — borrowed from proper-prepper.
22. **Made content the primary deliverable and tooling deliberately light**, fitting the good-deed
    definition (open content) rather than over-engineering an app.
23. **Added offline/printable output + RTL/offline-font i18n**, since last-mile WASH need coincides with
    poor connectivity and non-Latin scripts.
24. **Added an explicit borderline-scope open question** (where safe household ORS practice ends and
    clinical instruction begins, e.g., infants) for the expert to settle, rather than guessing.
25. **Tied every numeric claim to a specific cited source** (not a general "sources" list) so each dose
    is independently traceable and re-verifiable.

## Review sign-off

**Completeness check (against PLAN_SPEC §FILE 1).** All 17 required H2 sections are present and in the
specified order: Executive summary; Problem & beneficiaries; Goals and non-goals; Success metrics
(outcomes); Scope; Solution approach & architecture; Data, licensing & compliance; Quality, review &
risk gates; Roadmap & milestones; Work breakdown; Governance, roles & stakeholders; Dependencies &
integrations; Risks & mitigations; Security & privacy; Sustainability & maintenance; Open questions;
References. Metadata header present (Status/Version/Last updated/Owner/Lane). Appendix A (25 applied
improvements) and this sign-off appended.

**Correctness check (against CLAUDE.md + good-deed-definition).**
- *Public benefit, free, non-commercial, no harm, executable with review* — all five good-deed criteria
  satisfied: CC-BY content/MIT tooling; not-for-profit; refusal/scope guardrails; HIGH content gated on
  expert review. ✔
- *Risk tier handling* — medium overall with a correctly-gated HIGH sub-class; credentialed-expert
  sign-off required before merge for HIGH content per the definition. ✔
- *License/provenance rigor* — WHO CC BY-NC-SA-IGO non-relicensing trap addressed; emblems barred;
  paraphrase-and-cite default; per-source verification + CI copy check. ✔
- *Privacy* — zero person-level data; no telemetry; no identifiable imagery. ✔
- *Honest partner status* — partner, requestor, steward, and credentialed expert all marked
  `TO BE SECURED`; `verifiedNeed:false` in TASKS; dated outreach + hold/decision rules. ✔
- *Engineering conventions* — TypeScript/ESM/pnpm; MIT code / CC-BY content; CI gates. ✔

**Issues found and fixed during review.**
- Ensured **HIGH-risk units cannot be part of *any* shipped state** (including the generic-public-good
  state) without expert sign-off + numeric verification — clarified in *Definition of Shipped*.
- Ensured **translations of HIGH-risk units re-run numeric verification per language** (a translated
  dose is a new failure surface) — added to *Quality gates* and M3.
- Confirmed every numeric value is tied to a **specific** source, not the unit's general source list —
  reflected in the data model and improvement #25.

**Outstanding human decisions (cannot be resolved in-plan):** secure a credentialed expert reviewer
(M2 gate, by 2026-09-30); secure a distribution partner/steward (M4 gate); confirm priority
topics/languages once a partner is known. Until then the project builds as a generic public good and
holds at M1 if no expert is secured.

**Sign-off:** Plan is internally consistent, schema-aligned, and compliant with Elyos guardrails for
its risk tier. Ready for maintainer review. — *Senior staff engineer + TPM (drafting agent)*
