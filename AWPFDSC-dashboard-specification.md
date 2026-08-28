# AWPFDSC Dashboard — Specification

> **Purpose.** Specification for the AWPFDSC dashboard: a national demand-and-supply comparison for women's pelvic-floor and continence services in Australia. Instantiated from the AWPFDSC Dashboard Specification Template v1.0, itself derived from the Bayside Health Pelvic Floor & Continence Services Dashboard specification (AUPFHS, v1 deployed 28 May 2026).
>
> **Version.** Specification v1.0 · 28 August 2026
>
> **Author.** A/Prof J. Oliver Daly BSc (Hons) MBBS FRANZCOG CU AFRACMA CHIA GAICD

---

## 0. Document metadata

| Field | Value |
| --- | --- |
| Dashboard name (full) | AWPFDSC — Australian Women's Pelvic Floor Demand and Services Comparison |
| Dashboard name (short) | AWPFDSC |
| Version | v1 |
| Status | **v1 built and deployed** (static single-page build, 28 August 2026) |
| Domain | Pelvic floor and continence services for women — prolapse, urinary incontinence, faecal incontinence |
| Geography | Australia — national, stratified by ASGS Remoteness Area (RA 2021) and by state/territory |
| Sponsor / governance | AUPFHS |
| Audience | Clinical leadership, national service-planning working groups, UGSA and RANZCOG committees, jurisdictional health departments, consumer-advocacy partners |
| Confidentiality | Internal (no patient-level data; all inputs are published sources, so a public release is technically permissible subject to sponsor sign-off) |
| Companion document | *Australian Women's Pelvic Floor Care Needs and Health Services Supply* v1.0 (28 August 2026), delivered alongside this specification in markdown and PDF |
| Governance repo | ideasth/aupfhs-governance |
| Source code | ABC – Prolapse project file repository, `awpfdsc-dashboard/` |
| Live URL | Deployed private preview (see the delivery message for the current URL) |

### 0.1 As-built deviation from the template

The template's default six-tab pattern leads with **Map** and **Capability matrix**, both of which require a site-level inventory with coordinates and per-site capability flags. **No such national dataset exists.** The source research established that a national map requires linking at least three separate layers (AIHW hospital reporting units, the RANZCOG O&G Map, and jurisdictional outpatient dashboards), that the RANZCOG O&G Map is current only to July 2023, and that private-sector capability is not published at all in Tasmania, the ACT or the Northern Territory.

Building a Map tab from the available data would therefore have produced a facility map that misrepresents service availability. The as-built v1 substitutes two tabs that the data does support, and carries Map and Capability matrix into the v2.0 roadmap conditional on the national site inventory being assembled.

| Template tab | As-built v1 | Rationale |
| --- | --- | --- |
| 5.1 Map | **Deferred to v2.0** | No national site-level inventory with coordinates and capability flags exists |
| 5.2 Capability matrix | **Deferred to v2.0** | Same dependency; a site inventory is a prerequisite |
| — | **Overview** (new) | Headline KPIs, the two defining supply gradients, and the six structural findings |
| 5.4 Burden of disease | **Burden of disease** | Built as specified, plus the birth-cohort projection layer |
| — | **Workforce and supply** (new) | Substitutes the deferred capability matrix; NHWDS supports workforce-by-remoteness directly |
| — | **Access and waiting lists** (new) | The dominant access constraint in this domain is waiting time, which the template did not surface |
| 5.3 Gap analysis | **Gap analysis** | Built, but as a demand-to-supply-ratio surface rather than a drive-time surface |
| 5.6 Sources and methodology | **Sources and methodology** | Built as specified |
| 5.5 Service plan | Omitted | No accompanying published national planning document exists to summarise |

---

## 1. Overview

AWPFDSC is a static, single-page dashboard presenting a unified national demand-and-supply view of women's pelvic-floor and continence care in Australia. It renders estimated prevalent need, the three workforces that carry this care, the sector split in which care is delivered, and published waiting-time access, all stratified by ASGS Remoteness Area and by jurisdiction. Its purpose is to make one structural finding legible to governance and advocacy audiences: Australia has a large, well-characterised need and a small, highly metropolitan, predominantly private supply, and the misalignment worsens monotonically with remoteness. It is a demand-and-supply comparison rather than a service map, because the underlying national service-level dataset does not yet exist — a gap the dashboard itself documents.

---

## 2. Scope and boundaries

### 2.1 In scope

- **Clinical domain.** Assessment, conservative care, pelvic-floor physiotherapy, continence nursing, urodynamics, urogynaecology, and reconstructive pelvic-floor surgery for prolapse, urinary incontinence and faecal incontinence.
- **Geographic scope.** All Australian states and territories, at ASGS Remoteness Area (RA1–RA5, 2021) and state/territory resolution.
- **Population scope.** Women aged 18 and over. Women 65+ derived and available in the data model but not surfaced in v1.
- **Workforce scope.** General practitioners, obstetrician-gynaecologists, pelvic-health physiotherapists, and practitioners designating urogynaecology as their specialty.
- **Activity scope.** Reconstructive pelvic-floor procedures (SUI, apical/suspension prolapse, compartment prolapse), public gynaecology elective surgery, and published gynaecology outpatient waiting data.
- **Time horizon.** Current-state snapshot with mixed data vintages (see §9), annual refresh cadence.

### 2.2 Out of scope

- Patient-level data of any kind. No PHI, no identifiers, no clinical records.
- Real-time hospital-system feeds. All data is build-time baked.
- Paediatric continence, male pelvic floor.
- Mesh-complication revision activity — the procedure analysis is reconstructive-only by design.
- Named individual clinicians, and any site-level attribution of workforce.
- Site-level service mapping (deferred, see §0.1).

### 2.3 Explicit non-goals

- Not a clinical decision-support tool. No claim to clinical recommendation.
- Not a live capacity or waitlist management system.
- Not a substitute for jurisdictional health-service planning processes.
- Not a claim that the modelled prevalence figures represent an unmet-surgery shortfall — most prolapse is managed conservatively and should be.

---

## 3. Audience and use cases

| Audience segment | Primary use case |
| --- | --- |
| National service-planning working group | Quantify the remoteness gradient in specialist supply and locate the jurisdictions with no published outpatient waiting data |
| Jurisdictional health-department planners | Compare in-state gynaecology elective surgery performance against the national reference, and see local reliance on public versus private delivery |
| UGSA and RANZCOG committees | Subspecialty workforce distribution and training-post placement — all 10 accredited units are currently in major-city localities |
| RACGP and primary-care policy | Frame the unmeasured GP pelvic-floor capability question and the case for a Health of the Nation subquestion |
| Consumer advocacy partners | A single citable surface for the scale of need against delivered activity, and for the measurement gap itself |
| Individual clinician / researcher | Remoteness-level demand-to-supply estimation and a source register for onward work |

---

## 4. Architecture and technology

### 4.1 Tech stack — as built

The template's default Vite + React + TypeScript + Tailwind + shadcn stack was **deliberately not used** for v1. The build is a **single self-contained HTML file plus one baked JSON-as-JS data module**, with Chart.js from CDN for charts and hand-written CSS using the design tokens of the reference Bayside dashboard.

Rationale: v1 has no map, no routing, no global state and no interactive filters beyond tab selection. A framework build would add a toolchain, a `node_modules` tree and a bundle step for no functional gain, and would make the artefact harder to hand to a governance audience as a single file. If v2.0 adds the map and capability matrix, migrating to the template's reference stack becomes the right call and should be done at that point.

- **Frontend.** Static HTML5 + vanilla ES2020. No framework, no build step.
- **Styling.** Hand-written CSS with custom properties. Design tokens inherited from the Bayside reference dashboard palette (teal `#0f766e`, plum `#7c3f6d`, amber `#b45309`, red `#9f1239`, ink `#14213d`).
- **Charts.** Chart.js 4.4.1 via jsDelivr CDN — bar, stacked horizontal bar, line, doughnut, logarithmic-axis bar.
- **Cartography.** None in v1. Leaflet or MapLibre GL to be introduced in v2.0 with the site inventory.
- **State.** URL-hash tab routing (`#overview`, `#burden`, `#workforce`, `#access`, `#gap`, `#sources`) so any tab is directly linkable and screenshot-addressable. No other state.
- **Data.** Single `data.js` module assigning a frozen object to `window.AWPFDSC`, generated by `compute.py`. **No backend, no database, no PHI.**
- **Deployment.** Static bundle, deployed to a private preview URL.

### 4.2 Deployment model

- **v1 (read-only).** Static two-file bundle (`index.html`, `data.js`) plus this specification and the companion report. Build-time data only. Deployed to a private preview URL reachable only by the owner.
- **v2 (dual-build, optional).** If a private-full build becomes necessary (site-level workforce inference), gate content by build flag with private-only fields held in a gitignored data file pulled from the governance repo at build time. Not required at v1, because every input is already a published source.

### 4.3 Data pipeline — as built

1. **Ingest.** Source datasets deposited in the ABC – Prolapse project file repository by the five upstream analysis threads: `og-workforce-remoteness-2023/`, `gp-workforce-remoteness-2023/`, `physio-pelvichealth-workforce-2023/`, `urogyn-volumes-2023-24/`, `aihw-gynaecology-elective-surgery-*.csv`, `aus-gynaecology-outpatient-waits-national.csv`, `vic-gynaecology-outpatient-waits-2025Q2.csv`, and the baked dataset inside `workforce-comparison-charts/`. Plus two ABS workbooks retrieved directly for the adult-female denominator.
2. **Transform.** `compute.py` — a single Python script that assembles remoteness rows, derives per-100,000 supply, applies prevalence constants, computes demand-to-supply ratios and metropolitan concentration factors, and emits `awpfdsc-data.json`.
3. **Validate.** Per-100,000 figures and concentration factors cross-checked against the independently produced `workforce-comparison-charts/README.md` from the upstream workforce thread; remoteness populations reconciled to the national ERP total; console-error check on every tab via headless Chromium.
4. **Bake.** `awpfdsc-data.json` wrapped as `window.AWPFDSC` in `data.js`, loaded before the render script.
5. **Provenance.** `meta` block carries build date, the derived adult-female share, and the prevalence constants used. Every table and chart carries an inline source note naming the collection and its vintage.

---

## 5. Functional surfaces (tabs)

### 5.1 Overview

- Eight headline KPI cards: women 18+, the three prevalence estimates, national O&G headcount, designated urogynaecologists, reconstructive procedures delivered, and the Medicare-funded share.
- Grouped bar chart: O&G and pelvic-health physiotherapy supply per 100,000 by remoteness.
- Bar chart: prolapse-plus-incontinence cases per O&G specialist by remoteness, with Very Remote highlighted.
- The six structural findings as a numbered narrative block.

### 5.2 Burden of disease

- Three cohort KPI cards: women who gave birth in 2023, recorded third- or fourth-degree tears, and lifetime prolapse-surgery risk.
- **Prominent prevalence-floor caveat**, positioned above the charts, stating that prevalent cases are not new referrals and naming the help-seeking evidence.
- Logarithmic grouped bar chart of prevalent cases by remoteness and condition (log axis required to keep Very Remote legible against Major Cities).
- Doughnut chart of 2023 mode of birth.
- Prevalent-need table by remoteness with national footer row.
- Cohort projection table (20 / 30 / 40-year horizons) and a "where the risk comes from" aetiology panel.

### 5.3 Workforce and supply

- Four workforce KPI cards including DRANZCOG holders as the surrogate measure.
- Stacked horizontal bar: headcount distribution by remoteness as a percentage of each workforce.
- Bar chart: metropolitan concentration factor, with an explicit note that a value below 1 (general practice) means higher per-capita supply outside the cities.
- Line chart: sector reliance inverting with remoteness, with the confidentialised Remote and Very Remote O&G cells omitted rather than plotted as zero.
- Subspecialty capacity table.
- Full workforce table by remoteness area with national footer.
- Bounded-estimate bar panel for the GP pelvic-floor capability question, with the four DRANZCOG caveats stated in full.

### 5.4 Access and waiting lists

- Four access KPI cards including "jurisdictions publishing outpatient waits: 4 of 8".
- **Prominent non-comparability caveat** distinguishing wait-to-first-appointment from wait-to-surgery-after-listing, and stock from flow.
- Two bar charts: elective surgery median and 90th-percentile waits by jurisdiction, and admission volume by jurisdiction.
- Elective surgery table by jurisdiction with national footer.
- Outpatient reporting-availability table with colour-coded Yes / Partial / Historical / No pills and the detail for each publishing jurisdiction.
- Two ranked bar panels: highest proportion waiting over 365 days, and longest median waits, by local health network.
- Structural access-barrier panel. Service-specific practitioner-reported waiting figures are held in the private companion report and excluded from the published build.

### 5.5 Gap analysis

- Four gap KPI cards anchored on the Very Remote cases-per-specialist figure.
- Grouped bar chart: demand-to-supply ratio by remoteness for both O&G and pelvic-health physiotherapy.
- Stacked horizontal bar: public versus Medicare-funded delivery by procedure family.
- Procedure table with national footer.
- **Conversion funnel** — log-scaled horizontal bars from women 18+ through prevalent prolapse, help-seeking, procedures delivered, public procedures, and designated urogynaecologists. Log scaling is stated on the surface so the visual is not read as a linear comparison.
- Roadmap table: the nine prioritised actions that would make the gap measurable.

### 5.6 Sources and methodology

- Method panel: how each number is derived, including the derived adult-female denominator and its known bias direction.
- Known-limitations panel.
- Full source register with 22 entries, each with a live link.
- Attribution panel including the three corrections of record (UGSA not "AAUG"; the retired MyHospitals domain; lifetime risk ~1 in 5 rather than 1 in 8–12).
- Build-date footer on every tab.

---

## 6. Data model — as built

### 6.1 Site (clinical location)

**Not implemented in v1.** No national site inventory exists. The template schema is retained unchanged for v2.0. The Victorian 61-site proof-of-concept inventory from the upstream remoteness thread is the reference template for the national build, and confirms the schema is workable — it captured site name, parent service, remoteness class, advertised subspecialty status, and inpatient surgical capability.

### 6.2 Catchment unit — as built

Resolution is **ASGS Remoteness Area (RA1–RA5)**, not SA3 or LGA. This is a deliberate downward resolution choice: the workforce collection (NHWDS) publishes remoteness as a dimension but not SA3, so RA is the finest resolution at which supply and demand can both be measured from published data. SA3 resolution becomes available only once the site inventory exists.

| Field | Type | As-built value |
| --- | --- | --- |
| ra | string | Major Cities / Inner Regional / Outer Regional / Remote / Very Remote |
| pop | number | Total ERP at 30 June 2023 |
| women18 | number | **Derived** — national women-18+ share (38.59%) applied to `pop` |
| women65 | number | **Derived** — national women-65+ share (7.86%) applied to `pop`; computed but not surfaced in v1 |
| prev_ui / prev_pop / prev_fi | number | Prevalence constants applied to `women18` |
| gp / og / physio / urogyn | number | NHWDS 2023 headcount, in labour force in Australia |
| gp_per100k / og_per100k / physio_per100k | number | Supply per 100,000 total population |
| og_public_modal | number \| null | O&G public share of clinical hours, 35–49 h band. **Null where NHWDS confidentialises** |
| gp_excl_public | number | Proportion of GPs exclusively public |
| cases_per_og / cases_per_physio / pop_cases_per_og | number | Derived demand-to-supply ratios |
| cohort20 | number | Modelled 20-year first-prolapse-operation need from the 2023 cohort |

`area_km2` and `centroid` are omitted because v1 has no drive-time or map surface.

### 6.3 Prevalence constants — as built

| conditionCode | ratePerWomanAdult | Provenance |
| --- | ---: | --- |
| UI | 0.250 | Inherited from the AWPFDSC template §5.4, itself from the Bayside Health Pelvic Floor & Continence Services Dashboard |
| POP (symptomatic) | 0.068 | As above |
| FI | 0.198 | As above |

**Provenance gap, stated plainly.** These constants are inherited rather than re-derived from an Australian systematic review for this build. That is a real limitation and is named in §9 and on the dashboard's methodology surface. Re-deriving them against Australian population data is a v2.0 item.

Additional constant: **help-seeking multiplier 0.30 over 10 years**, applied only in the Gap analysis conversion funnel.

### 6.4 Indicator dataset — as built

Implemented as three separate baked arrays rather than one generic indicator table, because the three collections have incompatible units:

- `procedures[]` — procedure family, NHMD separations, MBS services, derived public, % Medicare-funded.
- `elective[]` — jurisdiction, admissions, median days, 90th-percentile days, % over 365 days.
- `outpatient[]` — jurisdiction, published status, native unit, metric, detail narrative.

The template's OASI indicator (PI13b) is carried as national cohort scalars (`cohort_oasi_2023`, `cohort_births_2023`, mode-of-birth percentages) rather than as a per-jurisdiction rate table, because the analysis needed the cohort denominator rather than a comparative rate.

### 6.5 Workforce inference

**Not implemented.** v1 uses published workforce headcount by remoteness directly and makes no site-level inference. Nothing in the build attributes workforce to a named site or clinician. Retained in the roadmap for v2.0 only if the site inventory is built, and then public-source-only.

---

## 7. Sources and citations

| Source | Feeds | URL | Licence | Retrieved |
| --- | --- | --- | --- | --- |
| NHWDS 2023, Health Workforce Data Tool | Workforce headcounts, remoteness, sector splits | https://hwd.health.gov.au/datatool/ | Commonwealth terms of use | Aug 2026 |
| ABS Regional population 2023–24, Table 3 | Population by Remoteness Area, ERP 30 June 2023 | https://www.abs.gov.au/statistics/people/population/regional-population/2023-24 | CC BY 4.0 | Aug 2026 |
| ABS National, state and territory population, June 2023, Table 8 | Adult-female share of population | https://www.abs.gov.au/statistics/people/population/national-state-and-territory-population/jun-2023 | CC BY 4.0 | Aug 2026 |
| AIHW National Perinatal Data Collection 2023 | Mode of birth, perineal status, OASI | https://www.aihw.gov.au/reports/mothers-babies/australias-mothers-babies/data | AIHW terms of use | Aug 2026 |
| AIHW procedures data cubes (NHMD) 2023–24 | Procedure separations by ACHI code | https://www.aihw.gov.au/reports/hospitals/procedures-data-cubes/contents/summary | AIHW terms of use | Aug 2026 |
| Services Australia Medicare item statistics | MBS-funded procedure volumes | http://medicarestatistics.humanservices.gov.au/statistics/mbs_item.jsp | Commonwealth terms of use | Aug 2026 |
| AIHW Elective surgery waiting times 2023–24 | Gynaecology admissions, median, p90, % over 365 days | https://www.aihw.gov.au/hospitals/topics/elective-surgery/waiting-times | AIHW terms of use | Aug 2026 |
| AIHW MyHospitals API | LHN-level gynaecology elective surgery; hospital locations | https://myhospitalsapi.aihw.gov.au/ | AIHW terms of use | Aug 2026 |
| AIHW non-admitted patient care | Non-admitted activity; absence of a national waiting collection | https://www.aihw.gov.au/hospitals/topics/non-admitted-patient-care | AIHW terms of use | Aug 2026 |
| VAHI Specialist Clinics | Victorian gynaecology outpatient waits by health service | https://vahi.vic.gov.au/reports/victorian-health-services-performance/specialist-clinics | Vic Government terms | Aug 2026 |
| Queensland Health specialist appointments performance | HHS-level outpatient access | https://www.performance.health.qld.gov.au/statewide-performance/planned-care/specialist-appointments-performance | Qld Government terms | Aug 2026 |
| SA Health Specialist Outpatient Waiting Time Report | Metro Adelaide gynaecology outpatient waits | https://www.sahealth.sa.gov.au/ | SA Government terms | Aug 2026 |
| Canberra Health Services waiting times report, Nov 2023 | ACT gynaecology outpatient waits (historical) | https://www.canberrahealthservices.act.gov.au/data/assets/pdf_file/0003/2358642/Waiting-times-Outpatient-and-Emergency-Dept-Report-November-2023.pdf | ACT Government terms | Aug 2026 |
| RANZCOG Annual Report 2022–23 | Certified urogynaecology subspecialists, trainees, training units | https://ranzcog.edu.au/wp-content/uploads/Annual-Report-2022-2023.pdf | RANZCOG terms | Aug 2026 |
| RANZCOG Media Kit | DRANZCOG holders | https://ranzcog.edu.au/wp-content/uploads/Media-Kit.pdf | RANZCOG terms | Aug 2026 |
| Australian O&G Supply and Demand Report, April 2026 | O&G and urogynaecology FTE by MMM | https://hwd.health.gov.au/resources/primary/o&g-compendium-report-april-2026.pdf | Commonwealth terms of use | Aug 2026 |
| HWD remoteness summary | Workforce FTE by remoteness | https://hwd.health.gov.au/resources/data/summary-remote.html | Commonwealth terms of use | Aug 2026 |
| RACGP Health of the Nation 2024 | GP practice-area self-report | https://www.racgp.org.au/FSDEDEV/media/documents/Health-of-the-Nation-2024.pdf | RACGP terms | Aug 2026 |
| Smith et al. 2010 | Lifetime risk of first prolapse operation (19% by age 85) | https://pubmed.ncbi.nlm.nih.gov/20966694/ | Publisher terms | Aug 2026 |
| Hals et al. 2010 | Nordic multicentre severe-tear reduction | https://pubmed.ncbi.nlm.nih.gov/20567163/ | Publisher terms | Aug 2026 |
| Australasian Pelvic Floor Procedure Registry | Registry precedent and public reports | https://www.monash.edu/medicine/sphpm/registries/apfpr | Monash terms | Aug 2026 |
| Continence Health Australia | Help-seeking behaviour | https://www.continence.org.au/ | Publisher terms | Aug 2026 |
| Healthdirect Service Finder / NHSD | Private clinic discovery layer (v2 dependency) | https://www.healthdirect.gov.au/australian-health-services | Commonwealth terms of use | Aug 2026 |
| RANZCOG O&G Map | Publicly funded O&G service layer (v2 dependency; current to July 2023) | https://ranzcog.edu.au/ | RANZCOG terms | Aug 2026 |
| AIHW hospitals portal (MyHospitals successor) | Hospital reporting units, locations, sector (v2 dependency) | https://www.aihw.gov.au/hospitals | AIHW terms of use | Aug 2026 |

---

## 8. Methodology notes

### 8.1 Drive-time proxy

**Not implemented in v1.** The template's haversine-times-road-speed proxy (RA1 60 km/h, RA3 70 km/h, RA5 90 km/h) requires site coordinates, which do not exist nationally. Retained unchanged for v2.0. Access in v1 is measured by published waiting time and by per-capita supply gradient instead — both of which are arguably better access measures for this domain than distance, because the binding constraint reported in practice is waiting time, not travel.

### 8.2 Prevalence application

- Prevalence rates applied to `women18` per remoteness area.
- Prevalent cases are **not** new referrals. All prevalence figures are flagged as the **prevalence floor**, both in the report and on the dashboard's Burden of disease tab.
- The help-seeking multiplier (default 30% of prevalent cases seeking care over 10 years) converts prevalence to a demand estimate and is applied **only** in the Gap analysis conversion funnel, never in the prevalence tables.
- Help-seeking evidence supporting the multiplier's conservatism: approximately 70% of Australians with incontinence do not seek help, and only about 1 in 6 have ever discussed it with a GP.

### 8.3 Adult-female denominator — the principal methodological assumption

Women aged 18 and over by remoteness are **derived, not published**. The national women-18+ share of total ERP (10,284,187 ÷ 26,652,777 = 38.59%) is applied uniformly to each Remoteness Area population.

Remote and Very Remote populations skew younger and more male than the national average. Their adult-female counts — and therefore prevalence estimates and demand-to-supply ratios — are likely **overstated by roughly 5–10%**. The direction of the error is conservative with respect to the central finding: correcting it would reduce estimated remote demand somewhat, but the supply gradient is measured directly and is unaffected. Sourcing an RA-level age-and-sex table would remove the approximation and is the **priority v2.0 data refinement**.

### 8.4 Catchment assignment

**Not implemented in v1.** Remoteness areas are used as pre-defined strata, not as catchments assigned to sites. Retained for v2.0.

### 8.5 Workforce inference

**Not implemented.** Published headcount by remoteness only. No site-level or individual-level inference, and no named individuals anywhere in the build.

### 8.6 Counting-rule discipline

Carried forward from the upstream analyses and enforced across every surface:

- NHMD counts **separations**; MBS counts **services**. Different units, and they diverge for day-surgery and multi-procedure episodes.
- Stock (patients waiting at a census date) versus flow (patients admitted over a period) are never compared.
- NR, NP and blank cells never mean zero. Western Health's suppressed (NP) 2023–24 gynaecology figures are shown as suppressed.
- NHWDS confidentialises small cells to multiples of 3–5. The 2023 Remote public column reading zero is a **confidentialisation artefact**, and is rendered as `null` and labelled "suppressed" rather than plotted.
- ACHI-to-MBS mapping is many-to-one for several items, so family-level totals are presented and per-item comparisons are not.
- All waiting figures are in days unless a source publishes only months, in which case the unit is stated inline.

### 8.7 Anonymisation

No site-level or individual-level attribution appears anywhere in v1, so no anonymisation wording is required. If v2.0 introduces the site inventory, the governance repo's pre-agreed anonymised wording for historical single-clinician services applies before any publication.

---

## 9. Known limitations

1. **No service-level national inventory.** Supply is measured by workforce registration location, not service location. A practitioner's registered location is not where a prolapse clinic runs.
2. **Adult-female denominator derived nationally, not by remoteness** — see §8.3. Remote and Very Remote prevalence likely overstated by 5–10%.
3. **Urogynaecology is not separately identifiable** in any national or jurisdictional collection. Every urogynaecology-specific figure is a workforce self-designation, an ACHI/MBS reconstruction, or an inference from a derived public share.
4. **Outpatient waiting data are not poolable.** Four jurisdictions publish nothing; the four that publish use four incompatible native units.
5. **Cohort projections are per-cohort, not annual demand,** and rest on coarse marginal-independence risk strata that must not be presented as patient-level prediction.
6. **Prevalence constants are inherited,** not re-derived from an Australian systematic review for this build.
7. **Private-sector supply is only partially visible,** and least visible in Tasmania, the ACT and the Northern Territory, none of which publish a private-hospital licensing register.
8. **Mixed data vintages** — NHWDS 2023, ABS 2023, AIHW 2023–24, VAHI 2025 Q2, Queensland June 2026. Comparisons within one dataset are sound; across datasets they carry a vintage caveat.
9. **No map and no capability matrix in v1** — see §0.1.
10. **Read-only.** Updates require regenerating `data.js` and redeploying.
11. **No PDF export inside the dashboard.** Stakeholder sharing relies on the companion report PDF and on tab screenshots; each tab is directly linkable by URL hash to make screenshot capture reproducible.
12. **CDN dependency.** Chart.js is loaded from jsDelivr. Vendoring it locally is a small, worthwhile v1.1 change for offline and archival robustness.

---

## 10. Roadmap

### 10.1 v1 — national demand-and-supply dashboard (**built, 28 August 2026**)

- Six tabs: Overview, Burden of disease, Workforce and supply, Access and waiting lists, Gap analysis, Sources and methodology.
- Remoteness-stratified demand and supply, jurisdictional access, procedure sector split, conversion funnel, source register.
- Companion report delivered in markdown and PDF.
- Quality gates met: zero console errors on every tab, cross-validated per-capita figures, full visual screenshot review of all six tabs before delivery.

### 10.2 v1.1 — hardening (small, near-term)

- Vendor Chart.js locally to remove the CDN dependency.
- Source an RA-level ABS age-and-sex table and replace the derived adult-female denominator (§8.3). Highest-value single change in the whole roadmap.
- Surface the women-65+ cohort, already present in the data model.
- Add a data-freshness banner with last build date and next planned refresh.
- Migrate to the ABC – Prolapse project file repository as the canonical source location, with `compute.py` alongside the built artefact.

### 10.3 v2.0 — service map and capability matrix (planned, dependency-gated)

**Gate:** requires the national site inventory. Build it by extending the Victorian 61-site inventory template to the remaining seven jurisdictions, cross-referenced against the AIHW hospital reporting-units file and the RANZCOG O&G Map, with private sites from the five jurisdictions that publish a licensing register and Healthdirect for the remainder.

- Map tab (Leaflet or MapLibre GL), capability matrix tab, drive-time proxy per template §8.1.
- Migrate to the template reference stack (Vite + React + TypeScript + Tailwind) at this point — the framework earns its cost once there is a map and interactive filtering.
- SA3-resolution catchment layer once site coordinates exist.
- Re-derive prevalence constants from Australian literature.

### 10.4 v2.1 — capacity simulator (planned)

- Per template §10.3: clinician hours by role and site, activity rates per role-hour, waitlist inputs, skill-mix toggles, throughput caps.
- Outputs: quarterly capacity versus demand, bottleneck identification, FTE shortfall to clear the waitlist within 12 months, wait-time projection at 6, 12 and 18 months.
- Ships with defaults labelled as model assumptions, and with defensibility caveats built into the UI.
- **Gate:** requires site-level workforce data that does not currently exist publicly.

### 10.5 Evidence-base actions (outside the dashboard, tracked here)

The nine prioritised actions in the Gap analysis tab's roadmap table, led by: a person-linked NPDC → admissions → MBS analysis with competing risks; a national outpatient waiting-list minimum data set; and a **sub-clinic code for urogynaecology within Gynaecology** in outpatient and elective collections. The last is the single lowest-cost, highest-leverage change, because it would make the gap measurable without building any new collection.

---

## 11. Quality and governance

### 11.1 Build quality gates — as applied to v1

- **Console errors:** zero, verified on all six tabs in headless Chromium.
- **Cross-validation:** per-100,000 supply figures and metropolitan concentration factors reproduced independently and reconciled against the upstream `workforce-comparison-charts/README.md`; remoteness populations reconciled to the national ERP total.
- **Visual review:** full-page screenshot of every tab inspected before delivery, specifically for text wrapping, overflow, axis-label collision, invisible bars on linear scales, and text-on-background contrast. Four defects found and fixed: KPI grid reflowed to an even 4+4, logarithmic axis ticks pinned to prevent label collision, the conversion funnel switched to log-scaled bar widths so small values remain visible across five orders of magnitude, and three wide tables switched to left alignment.
- **Not applied (not applicable to a no-framework build):** TypeScript compilation, bundle warnings, Playwright interaction suite. If v2.0 migrates to the reference stack, all three become mandatory.
- **Accessibility:** WCAG 2.1 AA colour contrast on text and on chart-legend labels; tab list uses `role="tablist"` with `aria-selected`; tabs are keyboard-reachable. **Not yet verified:** screen-reader traversal of chart canvases — charts should gain data-table fallbacks in v1.1.

### 11.2 Data-refresh governance

- **Cadence:** annual, tracking the NHWDS and AIHW release cycles. Out-of-cycle refresh warranted if AIHW introduces a urogynaecology sub-clinic code or any jurisdiction begins publishing non-admitted gynaecology waits.
- **Refresh owner:** AUPFHS clinical informatics lead (role, not individual).
- **Refresh log:** append-only markdown table in the governance repo, per the standing Space activity-log convention.

### 11.3 Change control

- Any change to the shape of the baked data object requires a version bump in `meta.version` and an entry in §14.
- Any change to a prevalence constant, the help-seeking multiplier, or the derived adult-female share requires an explicit note in §14 and a corresponding update to the report's methodology section — the two documents must not drift.
- Breaking changes to the tab hash routes require redirect handling, because hash URLs are the documented screenshot and citation mechanism.

---

## 12. Companion artefacts

- **Report.** *Australian Women's Pelvic Floor Care Needs and Health Services Supply* v1.0, 28 August 2026 — markdown and PDF. The narrative counterpart to this dashboard; every figure on the dashboard appears in the report with its full source citation.
- **Specification.** This document, v1.0.
- **Source datasets.** ABC – Prolapse project file repository, as listed in §4.3.
- **Upstream analyses.** Five ABC – Prolapse project threads: Obstetrics and Gynaecology Workforce Analysis; Public Data on Urogynaecology Waiting Lists; Urogynaecology Volumes and Demand Analysis; Australian Women's Health Services by Remoteness; Vaginal Prolapse Interview Questions.
- **Reference implementation.** Bayside Health Pelvic Floor & Continence Services Dashboard v1 — https://ideasth.github.io/BaysideHealth-PelvicFloorServicePlanningTool/
- **Not yet built** (offered but not commissioned in the upstream threads): a one-page PDF governance handout, and SA3/LHN-level supply-per-100,000 maps.

---

## 13. Open questions and decisions to confirm

1. **Publication status.** Every input is a published source and no patient-level data is used, so a public release is technically permissible. Confirm whether AWPFDSC v1 should be published publicly, and if so under what sponsor attribution.
2. **Licence.** Recommend CC BY 4.0 for the dashboard and report; source data retains upstream licences. Confirm.
3. **Adult-female denominator.** Confirm whether to commission the RA-level ABS age-and-sex table now (v1.1) or accept the derived approximation until v2.0.
4. **Prevalence constants.** Confirm whether to re-derive the three rates from Australian literature, or continue to inherit them from the Bayside specification with the provenance caveat stated.
5. **National site inventory.** Confirm whether to commission the seven-jurisdiction extension of the Victorian inventory template — this is the gate on the entire v2.0 map and capability surface, and is the largest single piece of work in the roadmap.
6. **Catchment resolution for v2.0.** SA3 (national comparability, ~350 units) versus LGA (jurisdictional familiarity, ~540 units). Recommend SA3.
7. **Private-site inclusion criteria for v2.0.** Published capability only, versus self-attestation. Recommend published capability only, and state plainly that this systematically under-counts private provision in Tasmania, the ACT and the Northern Territory.
8. **Lived-access content.** Service-specific practitioner-reported waiting figures are excluded from the public build and retained in the private companion report. Revisit only if an auditable source becomes available for the four jurisdictions that publish nothing.

---

## 14. Change log

| Version | Date | Author | Notes |
| --- | --- | --- | --- |
| Template v1.0 | 2026-08-28 | A/Prof J. Oliver Daly | Initial template derived from the Bayside Health Pelvic Floor & Continence Services Dashboard specification (v1, 28 May 2026). |
| Spec v1.0 | 2026-08-28 | A/Prof J. Oliver Daly | AWPFDSC instantiation. Documents the as-built deviation from the template's six-tab pattern (§0.1): Map and Capability matrix deferred to v2.0 for want of a national site inventory; Overview, Workforce and supply, and Access and waiting lists substituted. No-framework static build adopted for v1 in place of the reference Vite/React stack, with a documented migration trigger. Catchment resolution set to ASGS Remoteness Area rather than SA3. Adult-female denominator documented as the principal methodological assumption. |

---

## Appendix A — Attribution

This specification instantiates the *AWPFDSC Dashboard Specification Template* v1.0 (A/Prof J. Oliver Daly, 28 August 2026), which is itself derived from the *Pelvic Floor & Continence Services Dashboard* specification (Bayside Health LHSN, AUPFHS, v1 deployed 28 May 2026), authored by A/Prof J. Oliver Daly. That reference specification is available in the AUPFHS governance repository and, in its v1 deployed instance, at [ideasth.github.io/BaysideHealth-PelvicFloorServicePlanningTool](https://ideasth.github.io/BaysideHealth-PelvicFloorServicePlanningTool/).

The AWPFDSC instantiation extends the regional Bayside model to a national, remoteness-stratified footprint and inherits the same read-only, no-PHI, static-bundle architecture. It substitutes a demand-and-supply comparison for the reference model's service map, because the national site-level dataset the map would require does not yet exist — a gap this dashboard documents rather than papers over.
