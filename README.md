# AWPFDSC — Australian Women's Pelvic Floor Demand and Services Comparison

A static dashboard comparing pelvic-floor and continence **care need** against **health
service supply** for Australian women, by ASGS Remoteness Area and jurisdiction.

**Live dashboard:** https://ideasth.github.io/AWPFDSC-Dashboard/

Version 1.0 · 28 August 2026 · A/Prof J. Oliver Daly

## What it shows

Six tabs:

| Tab | Content |
| --- | --- |
| Overview | Headline need and supply counts, per-capita supply gradient, caseload per specialist |
| Burden of disease | Prevalent need by remoteness, 2023 birth cohort, modelled downstream demand |
| Workforce & supply | O&G, GP and pelvic-health physiotherapy supply; subspecialty capacity; sector split |
| Access & waiting lists | Public elective surgery by jurisdiction; what outpatient waiting data each jurisdiction publishes |
| Gap analysis | Demand-to-supply ratios and the funnel from prevalence to delivered procedures |
| Sources & methodology | Full source register with links, derivations, and limitations |

## Headline findings

- Approximately **699,000** Australian women have symptomatic pelvic organ prolapse,
  **2.57 million** have urinary incontinence and **2.04 million** have faecal
  incontinence, on accepted prevalence rates applied to the 10.28 million women aged 18
  and over.
- Australia has **1,884** obstetrician-gynaecologists, **2,471** pelvic-health
  physiotherapists and **36** practitioners who designate urogynaecology as their
  specialty. All **10** accredited urogynaecology training units are in major-city
  localities.
- O&G supply per capita in Major Cities is **5.3 times** that of Very Remote Australia.
  Each O&G specialist in Very Remote Australia notionally carries **8,102**
  prolapse-and-incontinence cases against 1,541 in Major Cities.
- About **72%** of reconstructive pelvic-floor surgical activity is Medicare-funded, so
  the access question is as much cost as waiting.
- **Urogynaecology cannot be separated out of any Australian national or jurisdictional
  dataset.** It is bundled into "Gynaecology" everywhere, so the gap this dashboard
  describes is not routinely measured.

## Data sources

All figures come from published Australian sources — NHWDS 2023 via the Health Workforce
Data Tool, ABS Estimated Resident Population at 30 June 2023, AIHW NHMD and elective
surgery waiting times 2023–24, AIHW National Perinatal Data Collection 2023, Services
Australia Medicare item statistics, RANZCOG annual reporting, and state outpatient
dashboards. Every source is listed with its URL on the dashboard's Sources tab and in
`AWPFDSC-dashboard-specification.md`.

## How to run it

No build step and no dependencies to install. Open `index.html` directly, or serve the
folder:

```bash
python3 -m http.server 8000
```

Chart.js loads from a CDN, so rendering the charts needs a network connection.
`data.js` holds every value as `window.AWPFDSC` — edit it there, not in the markup.

## Important cautions

- **Prevalence-derived counts are a prevalence floor, not a referral stream.** Most
  prolapse is managed conservatively, and should be.
- **Cohort projections are per-cohort, not annual demand.** Every prior birth cohort is
  still generating need concurrently, so actual annual demand is substantially higher.
- **Risk strata behind the cohort model are an advocacy model**, built on
  marginal-independence assumptions. They are not patient-level predictions and must not
  be quoted as individual risk.
- **Supply is measured by workforce location, not service location.** A practitioner's
  registered location is not the same as where a prolapse clinic runs. There is no
  national service-level inventory.
- **Adult-female counts by Remoteness Area are derived**, by applying the national
  women-18+ share of total population (38.59%) uniformly. Remote and Very Remote figures
  are likely overstated by roughly 5–10%.
- **Outpatient waiting data are not poolable** across jurisdictions; four publish nothing
  and the four that publish use incompatible units.
- This is **not** a clinical decision-support tool, not a live capacity or waitlist
  system, and not a substitute for jurisdictional service planning. It contains **no
  patient-level data**.

## Scope of this repository

This repository holds the dashboard and its specification. The full companion analytical
report, including practitioner-reported service-specific material, is held privately and
is not published here.

## Licence

Code and presentation: MIT (see `LICENSE`). The underlying statistics remain subject to
the licence terms of their original publishers, predominantly Creative Commons
Attribution licensing for ABS and AIHW material.
