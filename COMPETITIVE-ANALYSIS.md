# Competitive & Improvement Analysis — wash-guides

> Scope: open, plain-language, multilingual WASH (water, sanitation, hygiene) how-tos sourced to
> authoritative bodies (WHO, UNICEF, CDC, Sphere) for low-resource + humanitarian settings.
> Public-health stakes: wrong water-treatment/sanitation/ORS guidance directly causes illness or death.
> Analysis date: 2026-06-29. Web-researched competitor claims are cited inline.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually mature for a v0.1 draft: it is internally consistent against the Elyos
good-deed rules, names the right authorities, and — critically for a public-health project — it does
**not** treat itself as uniformly "medium risk." The split into **medium overall + an explicit HIGH
sub-class** (ORS/dehydration, chemical water-treatment dosing) with credentialed-expert sign-off,
independent numeric second-checking, and a persistent "not a substitute" disclaimer is the single
most important correctness decision and it is handled well. Strengths and gaps by dimension:

**Sourcing to authoritative WASH guidance — STRONG, one gap.** WHO (GDWQ, sanitation, hand hygiene,
HWTS), UNICEF, CDC, and the Sphere Handbook are all named, with per-source license verification and a
documented **source-divergence precedence** (WHO for clinical/health; CDC for US context; Sphere/WASH
cluster for humanitarian; state divergence rather than average a safety-critical number). This is
correct and rare. **Gap:** the plan omits several first-tier open WASH bodies that are both sources
*and* competitors — **CAWST** (the world's largest open WASH e-library, see §2), **Hesperian**
(already plain-language, low-literacy, multilingual, freely reusable — the closest competitor), the
**Global WASH Cluster** (humanitarian hygiene-promotion toolkit), and **Akvopedia/IRC**. These should
appear in *Dependencies & integrations* as reference sources and partnership targets, not just WHO/
UNICEF/CDC/Sphere/IFRC.

**Accuracy of high-stakes specifics — gating is correct; one classification inconsistency.**
- *Chlorination.* Correctly HIGH-risk. WHO household guidance targets **free chlorine residual ≥0.5
  mg/L after ≥30 min contact at pH <8.0**, and ≥0.2 mg/L at point of use; CDC household emergency
  dosing is ~2 drops of 5–6% unscented bleach per litre (8 drops/gallon), 30-min wait
  ([WHO GDWQ Annex 3](https://cdn.who.int/media/docs/default-source/wash-documents/water-safety-and-quality/dwq-guidelines-4/gdwq4-with-add1-annex3.pdf),
  [CDC](https://www.cdc.gov/yellow-book/hcp/preparing-international-travelers/water-disinfection-for-travelers.html)).
  These are exactly the kind of value where "fabricated dose = poisoning or unsafe water," so the
  numeric-verification + expert-confirm gate is appropriate.
- *SODIS.* **Internal inconsistency to fix.** Scope (PLAN L140–141) lists "SODIS conditions" inside
  the HIGH-risk dosing sub-set, but TASKS `content-009` ships "SODIS … method-level, no dosing" as a
  **medium-risk M1** unit. SODIS carries safety-critical numerics — clear PET bottle ≤2–3 L, **≥6 h
  full sun / 2 consecutive days if cloudy**, turbidity threshold (<30 NTU), and the limit that SODIS
  does **not** remove chemical contamination
  ([CDC Yellow Book](https://www.cdc.gov/yellow-book/hcp/preparing-international-travelers/water-disinfection-for-travelers.html),
  [Akvopedia SODIS](https://www.akvopedia.org/wiki/UV_treatment_/_Solar_disinfection_(SODIS))). Decide
  explicitly whether SODIS exposure time/turbidity is a HIGH numeric claim or a reviewed-medium method;
  right now it is both.
- *Handwashing.* Medium-risk is correct; specifics (≥20 s scrub, the "critical times," ≥60% alcohol
  sanitizer fallback) are non-controversial
  ([CDC Clean Hands](https://www.cdc.gov/clean-hands/about/index.html)).
- *Latrine siting.* The plan covers latrine use/maintenance but does **not** surface the headline
  safety numeric beneficiaries most need: **latrines ≥30 m horizontally from any groundwater source,
  and pit base ≥1.5 m above the water table** (Sphere)
  ([Sphere 2018 WASH](https://spherestandards.org/wp-content/uploads/Sphere-Handbook-2018-EN.pdf)).
  This is itself a HIGH-stakes numeric (wrong siting contaminates the water supply) and should be
  explicitly risk-classed, not left implicit in "latrine maintenance."
- *ORS.* Correctly HIGH-risk (clinician sign-off). **Accuracy nuance the expert must settle:** WHO/
  UNICEF current standard is the **pre-packaged low-osmolarity ORS sachet**; the homemade salt-sugar
  solution (~6 level tsp sugar + ½ tsp salt per 1 L clean water) is a **fallback when sachets are
  unavailable**, and over-concentration is dangerous
  ([CDC ORS](https://www.cdc.gov/global-water-sanitation-hygiene/media/pdfs/ors_seasia_508.pdf),
  [WHO ORS](https://www.who.int/publications/i/item/WHO-FCH-CAH-06.1)). The plan's open question #8
  (where household ORS ends and clinical instruction begins, esp. infants) is the right hook for this.

**Expert review — STRONG.** Hard CI/governance gate (`riskClass:high` ⇒ recorded `expertSignOff` or
build fails), version-scoped sign-off, distinct credential bars (environmental-health/REHS for dosing;
licensed clinician for ORS), expert veto, and a dated hold rule (no expert by 2026-09-30 ⇒ hold at
M1). This matches the CLAUDE.md `risk-tier` requirement.

**Humanitarian-vs-development context — PARTIAL.** The plan acknowledges both settings and the
Sphere/WASH-cluster precedence for emergencies, but the *content schema* has no `context` field
(humanitarian/displacement vs. stable development). The same topic diverges by context — e.g.,
emergency chlorination targets a higher residual (~1.0 mg/L FRC in cholera/outbreak settings per Oxfam
WASH practice) than steady-state supply
([Oxfam WASH](https://www.oxfamwash.org/chlorination-in-emergencies/)). Add `context` to `WashUnit` so
a unit cannot be mis-served across settings.

**"Not a substitute" boundary — STRONG but widen the audience.** The disclaimer and out-of-scope
guardrail (no diagnosis/treatment/IV/medication dosing; link out) are well drawn. Consider adding
"**not a substitute for your local public-health authority / WASH practitioner**" explicitly — local
water chemistry, source type, and outbreak status can override generic guidance.

**Currency/staleness — STRONG.** `lastReviewed`/`validUntil` with auto-flag and withholding of expired
HIGH units is best-in-class and beats every competitor (static PDFs go stale silently).

**Multilingual & cultural — STRONG.** Safety-accuracy translation review (numbers/doses/danger-signs/
step order re-verified per language, not just fluency), RTL, offline fonts, and a cultural/dignity gate
for sanitation + MHH are all correct and well above sector norm.

**Net:** Plan is sound. The two correctness items worth fixing before M1/M2: (a) the **SODIS
medium/high classification contradiction**, and (b) **add a `context` field** (and surface the
latrine-siting numeric as a classified high-stakes value).

---

## 2. Competitive landscape

| Source / project | What it is | Strengths | Weaknesses (the gap we exploit) |
| --- | --- | --- | --- |
| **WHO Guidelines for Drinking-water Quality / sanitation / HWTS** | The global normative authority | Definitive; the citation everyone defers to | Long technical PDFs; English-dominant; `CC BY-NC-SA 3.0 IGO` (non-commercial, share-alike — **not** freely re-licensable); above the literacy level of end users |
| **WHO/UNICEF JMP (washdata.org)** | Global WASH monitoring/statistics | Authoritative data on the *scale* of need (2.1 B without safely-managed water; 3.5 B without safely-managed sanitation) | It is **data, not how-to guidance** — proves the need, doesn't meet it |
| **Sphere Handbook (2018)** | Humanitarian minimum standards | The reference for emergency WASH numerics (latrine 30 m / 1.5 m, water quantity) | Practitioner-facing, not household-facing; freely available but copyrighted; English-led |
| **CDC Healthy Water / Global WASH** | US-gov public-health guidance | Clear, often **public-domain** (US-gov work) → most reusable; good posters/ORS/handwashing assets | US-context default; not multilingual at scale; embedded third-party figures need per-asset check |
| **Hesperian** (*Where There Is No Doctor*, *Sanitation and Cleanliness for a Healthy Environment*) | NGO health/WASH guides for lay people | **Closest competitor:** already plain-language, low-literacy, heavily illustrated, **multilingual**, and **freely copyable** ("free or at cost, not for profit") | Book-/chapter-shaped, not a structured per-unit dataset; its license is *non-commercial* (not CC-BY); slower update cadence; not CI-gated/numeric-verified per claim ([Hesperian](https://hesperian.org/books-and-resources/), [Wikipedia](https://en.wikipedia.org/wiki/Hesperian_Health_Guides)) |
| **CAWST** | Calgary WASH charity + eng. firm | **World's largest open WASH e-library** — 3,000+ resources, 13 languages, biosand-filter & HWTS knowledge bases, offline mobile app, live expert chat ([cawst.org/resources](https://www.cawst.org/resources)) | Practitioner-/trainer-oriented; not a clean per-unit open dataset; not built around lay-household plain-language units with machine-checkable provenance |
| **Global WASH Cluster** | UN humanitarian coordination body | Field-tested hygiene-promotion toolkit; the gateway to humanitarian partners/adoption ([washcluster.net](https://www.washcluster.net/resource)) | Coordinator-facing tools, not beneficiary how-tos; **a partnership target, not a rival** |
| **Akvopedia / IRC WASH** | Open, editable WASH wiki + knowledge centre | Wiki-open, broad technical coverage (water/sanitation/sustainability portals) ([akvopedia.org](https://akvopedia.org/wiki/Water_Portal), [ircwash.org](https://www.ircwash.org/)) | Technology/engineering-leaning; variable plain-language quality; no per-claim expert sign-off or numeric-verification gate |

**Reading of the field:** Authoritative *content* is plentiful but fragmented, technical, English-led,
and license-restricted (WHO). Two players already do "plain-language + multilingual + freely reusable"
well — **Hesperian** (lay-household) and **CAWST** (practitioner/trainer). Nobody combines: structured
per-unit data + CI-enforced provenance + per-numeric expert verification + staleness fail-safe +
CC-BY-4.0 + offline/printable + safety-reviewed translation. That intersection is open.

---

## 3. Gaps we can fill

1. **A machine-checkable, per-unit open dataset** (vs. PDFs/books/wikis): every claim carries a named
   citation + retrieval date + verified license, enforced in CI — uniquely auditable.
2. **CC-BY-4.0 content** (truly unrestricted reuse, incl. commercial/derivative): Hesperian is
   non-commercial; WHO is `CC BY-NC-SA 3.0 IGO`. A clean CC-BY corpus paraphrased from facts (facts
   aren't copyrightable) is genuinely scarce.
3. **Per-numeric independent verification + credentialed-expert confirmation** on every dose/ratio/
   contact-time — no competitor exposes this as a gate.
4. **Staleness fail-safe** that withholds expired HIGH-risk dosing — competitors' PDFs go stale
   silently.
5. **Offline-first, printable, low-literacy, RTL, bundled-font** rendering for the exact last-mile
   (poor connectivity) where need is highest.
6. **Safety-accuracy-reviewed translation** (numbers/doses/danger-signs re-verified per language),
   prioritizing low-resource languages WHO/CDC don't cover.
7. **Context-tagged guidance** (humanitarian vs. development) so the same topic isn't mis-applied —
   nobody surfaces this cleanly to households.
8. **Harmonized cross-source units** that resolve (and explicitly state) divergence between WHO/CDC/
   Sphere on a single safety-critical number, instead of leaving the reader to reconcile three PDFs.

---

## 4. Differentiators to win

- **"Verifiable open WASH guidance."** Every number is traceable to a cited source, second-checked,
  expert-confirmed, and CI-gated — provenance as a *product feature*, not a footnote. This is the
  defensible moat against Hesperian/CAWST/Akvopedia.
- **Truly free reuse (CC-BY-4.0 + MIT)** with a clean paraphrase-from-facts pipeline that sidesteps the
  WHO `CC BY-NC-SA-IGO` trap and Hesperian's non-commercial limit.
- **Last-mile by design:** offline, printable, low-literacy, RTL, multilingual — built for the
  connectivity profile of the beneficiary, not the donor's browser.
- **Living, not static:** versioned units with `validUntil` and auto-withholding beat the sector's
  stale-PDF default.
- **Reusable across siblings** (the sourced-health-info engine, §7) — one provenance/verification
  pipeline serves first-aid, food-safety, water-quality, and translations.

---

## 5. Claude API leverage (and the hard limits)

**Where Claude helps (drafting + scale, human-gated):**
1. **Plain-language drafting from authoritative sources with inline citations.** Given a WHO/CDC/Sphere
   passage, Claude paraphrases facts into short, controlled-vocabulary, low-literacy steps and emits a
   structured `WashUnit` draft with `sources[]` and proposed `numericClaims[]` pre-tagged for human
   verification — accelerating authoring without copying text (respecting the CC-BY-NC-SA-IGO boundary).
2. **Translation + back-translation for the safety-accuracy review.** Claude drafts a target-language
   unit *and* back-translates numbers/doses/danger-signs/step-order for the human reviewer to diff —
   surfacing the exact failure surface (a flipped digit, a dropped "do not") without replacing the
   competent-speaker + safety reviewer.
3. **Context adaptation + divergence detection.** Claude flags where a unit's numbers differ between
   humanitarian vs. development context, or where WHO/CDC/Sphere disagree on a safety-critical value,
   and drafts the "sources differ — see both" note for expert adjudication.

Supporting uses: readability scoring/controlled-vocabulary linting, citation-coverage gap-finding,
copy/similarity pre-screen against source text, and glossary/controlled-vocabulary maintenance.

**Where Claude must NOT decide (hard guardrails):**
- **Never originate or "fill in" a WASH numeric** — chlorine concentration, FRC target, contact time,
  SODIS exposure, latrine distance, ORS ratio. Every number must come from a **cited source**, be
  **second-checked by a non-author human**, and **expert-confirmed**. No fabricated/interpolated/
  "rounded for simplicity" doses. CI fails any numeric lacking `verifiedBy` + `expertConfirmed`.
- **Never set or override risk classification or context** (medium/high; humanitarian/development) as
  the final word — Claude may propose; the documented policy + human reviewer decide.
- **Never approve, sign off, or substitute for the credentialed expert or the cultural/dignity
  reviewer.** Claude output is always a *draft*; HIGH units don't ship without recorded human
  `expertSignOff`.
- **Never cross the scope line into clinical instruction** (diagnosis, treatment, IV, medication
  dosing) — it must refuse and link out, per CLAUDE.md refusal guardrails.
- **Always carry the "informational, not a substitute for professional medical care, trained WASH
  practice, or your local public-health authority" framing** and flag high-risk content rather than
  smoothing it into confident prose.

The funded lane (if ever used) must respect the hard per-task budget cap and never run headless on
HIGH content — donated-lane human-in-the-loop is the default for this project.

---

## 6. Ten concrete optimizations

1. **Resolve the SODIS classification contradiction** (PLAN scope = HIGH dosing vs. TASKS `content-009`
   = medium method) — pick one rule and document it in the risk-classification ADR.
2. **Add a `context` field** to `WashUnit` (`humanitarian | development | both`) and require it; gate
   so a unit can't render outside its validated context. Tie emergency-vs-steady chlorination targets
   to it.
3. **Promote latrine-siting numerics to explicit classified values** (≥30 m from groundwater, pit base
   ≥1.5 m above water table, downhill/down-gradient of wells) with Sphere citations — don't bury them
   in "maintenance."
4. **Add CAWST, Hesperian, Global WASH Cluster, Akvopedia/IRC to Dependencies & integrations** as
   reference sources and partnership targets (Global WASH Cluster is the fastest route to a real M4
   adopting partner).
5. **Encode the WHO ORS-sachet-first / homemade-fallback hierarchy** as a structured rule in the ORS
   unit (sachet preferred; SSS only when unavailable; over-concentration danger; infant caveat) for
   the clinician to confirm.
6. **Build a "divergence record" type** in the schema so a unit can cite two authorities and render
   "sources differ — both shown" for any safety-critical number, per the existing precedence rule.
7. **Ship a pictogram/visual track early** (openly-licensed or commissioned) — low-literacy value
   collapses without visuals; resolve open question #7 in M0/M1, not later.
8. **Add a back-translation diff step** to the translation CI/review flow so numeric/danger-sign drift
   is mechanically surfaced per language.
9. **Publish a public "provenance & verification" page** per unit (sources, retrieval dates, verifier,
   expert, `validUntil`) — turn the audit trail into a trust differentiator competitors lack.
10. **Pre-register the FRC/contact-time/SODIS/ORS/latrine numerics as a "golden numeric set"** with a
    CI test asserting each rendered value still matches its cited source string — defends against silent
    edits (the top content-integrity threat in §Security).

---

## 7. Parallel & perpendicular spin-offs

- **first-aid-open** (parallel): same HIGH-risk gating, clinician sign-off, danger-signs, "not a
  substitute" framing. The ORS/dehydration unit literally straddles both projects — shared expert pool
  and shared schema.
- **water-quality-explainers** (perpendicular): plain-language explanations of *why* (turbidity,
  pathogens, FRC, contamination pathways) that the how-tos link to; reuses citations and JMP data.
- **food-safety-open** (parallel): handwashing/critical-times, surface disinfection, safe storage
  overlap directly; same plain-language + numeric-verification engine.
- **vital-info-translations** (perpendicular): the safety-accuracy translation pipeline (back-
  translation diff, numeric re-verification, RTL/offline fonts) generalizes to any high-stakes public
  info.
- **Reusable "sourced-health-info engine"** (the strategic asset): the schema (`sources[]` +
  `numericClaims[]` + `expertSignOff` + `validUntil`), CI gates (citation-coverage, no-self-approval,
  numeric-verification, copy/similarity, no-egress), and offline/printable renderer are domain-agnostic.
  Extract them into a shared Elyos package so every sourced-content good-deed inherits provenance +
  expert-gating for free.
- **Partnerships:** Global WASH Cluster (humanitarian adoption + field validation), CAWST (co-
  distribution via the largest WASH library + offline app), Hesperian (translation/illustration reuse
  under compatible terms), ministry-of-health WASH units, and community-health-worker networks.

---

## 8. Open questions

1. **SODIS risk class:** is SODIS exposure-time/turbidity a HIGH numeric claim or a medium reviewed
   method? (Resolve before M1 ships `content-009`.)
2. **Context field:** do we ship per-context unit variants, or one unit with context-tagged numerics?
   Affects schema + renderer.
3. **Latrine-siting:** classify the 30 m / 1.5 m numerics as HIGH? Do they need EH-expert sign-off like
   chlorination?
4. **ORS scope line for infants:** where exactly does safe household ORS end and clinical instruction
   begin? (Plan's open question #8 — needs the clinician.)
5. **Emergency vs. steady-state dosing:** do we publish both chlorination targets, and how do we stop a
   user applying the wrong one? (Ties to #2.)
6. **License compatibility with Hesperian/CAWST** for any visual/illustration reuse (their
   non-commercial terms vs. our CC-BY-4.0 output) — verify before embedding anything.
7. **Pictogram sourcing** (open set vs. commission) — unresolved and on the critical path for
   low-literacy value.
8. **Which partner first** — Global WASH Cluster vs. a single NGO vs. a ministry WASH unit — drives
   priority topics, languages, and context, all currently `TO BE SECURED`.

---

### Source list (web-researched)

- WHO GDWQ Annex 3 (chemical/chlorine): https://cdn.who.int/media/docs/default-source/wash-documents/water-safety-and-quality/dwq-guidelines-4/gdwq4-with-add1-annex3.pdf
- CDC Water Disinfection (chlorination, SODIS): https://www.cdc.gov/yellow-book/hcp/preparing-international-travelers/water-disinfection-for-travelers.html
- CDC Clean Hands / handwashing: https://www.cdc.gov/clean-hands/about/index.html
- CDC ORS how-to: https://www.cdc.gov/global-water-sanitation-hygiene/media/pdfs/ors_seasia_508.pdf
- WHO Oral rehydration salts: https://www.who.int/publications/i/item/WHO-FCH-CAH-06.1
- Sphere Handbook 2018 (WASH, latrine siting): https://spherestandards.org/wp-content/uploads/Sphere-Handbook-2018-EN.pdf
- Oxfam WASH chlorination in emergencies: https://www.oxfamwash.org/chlorination-in-emergencies/
- Akvopedia SODIS: https://www.akvopedia.org/wiki/UV_treatment_/_Solar_disinfection_(SODIS)
- WHO/UNICEF JMP (washdata.org): https://washdata.org/ ; 2025 report: https://data.unicef.org/resources/jmp-report-2025/
- CAWST resources: https://www.cawst.org/resources
- Hesperian books & resources: https://hesperian.org/books-and-resources/ ; https://en.wikipedia.org/wiki/Hesperian_Health_Guides
- Global WASH Cluster resources: https://www.washcluster.net/resource
- Akvopedia / IRC WASH: https://akvopedia.org/wiki/Water_Portal ; https://www.ircwash.org/
