# TerraWise

> **T**erritorial **E**mergency **R**isk & **R**esilience **A**nalytics — **W**arning, **I**ntelligence, **S**imulation & **E**valuation.

TerraWise is **Infordata Sistemi**'s territorial-emergency platform: a digital twin that pairs live risk monitoring, AI-driven warning and physics-grounded fire-spread simulation to help authorities prevent, anticipate and respond to wildfires today — and to the wider family of territorial emergencies (flood, heat, slope instability, compound risk) tomorrow.

This repository is the **public umbrella** — what TerraWise is, how the modules fit together, where to find each one, and where the product is going. The implementation lives in the family of `kf50-*` repositories (see [MODULES.md](MODULES.md)).

---

## The four capabilities (today)

| Pillar | What it does | Today in production |
|---|---|---|
| **Warning** | Detect early signals — VOC e-noses, thermal IR cameras, satellites, citizen reports — and turn them into prioritised alerts | Karst Firewall 5.0 operational cockpit · alerting via email / SMS / WhatsApp |
| **Intelligence** | Score risk at street level by fusing Karst-calibrated fire-weather (FWI) and a machine-learning ignition model | KFWI: **77.5%** fire detection vs **29%** baseline; ignition model AUC **0.934** |
| **Simulation** | Forward-simulate fire spread on the live digital twin — Huygens propagation over a Rothermel surface-fire model | [PyroWISE](https://github.com/infordata-sistemi/pyrowise) engine; nowcasts on demand and pre-computed scenarios |
| **Evaluation** | Compare forecasts to outcomes; validate prevention investments with measurable evidence | Post-incident IoU against observed perimeters; 30-year burned-area baseline (Sentinel/Landsat) |

---

## The five ambitions (where TerraWise is going)

> A summary of [ROADMAP.md](ROADMAP.md). The most accessible, living version with rationale and recommended-first-move tagging is at [karst-map.way.to.it/portal/roadmap](https://karst-map.way.to.it/portal/roadmap) (IT · SL · EN · DE) — this section is its English mirror, structured for engineers and procurement teams.

Four shifts shape everything below:

1. From **a single hazard** (fire) to **many**.
2. From **static maps** to **living data** that updates itself.
3. From **a finished tool** to **a modular platform** others can build on.
4. From **one plateau** (the Karst) to **a sea** (the Mediterranean).

### Pillar 1 — Multi-hazard

> *From a wildfire twin to a multi-hazard twin — the same living digital twin reads flood, heat, slope and seismic risk, and where they overlap on the same people and assets.*

| Direction | Horizon | Why it's interesting |
|---|---|---|
| ★ **Flooding & flash floods** | Now | Pluvial + flash-flood exposure from rainfall, terrain hydrology and karstic underground drainage. Reuses the existing weather network + 3D terrain. |
| ★ **Extreme heat & "heat bombs"** | Now | Heat-wave + urban-heat exposure from station network + land cover. Public-health early warning *and* a fuel-drying signal for the fire model. |
| Slope instability & landslides | Next | Landslide susceptibility from slope, soil and rainfall — sharpened after fires when burnt ground sheds water. Natural pair with post-fire recovery. |
| Seismic & compound risk | Next | Overlay seismic hazard and cross-correlate the layers into one **compound-risk index** — where fire, flood, heat and earthquake stack on the same zone. The multi-hazard payoff. |

### Pillar 2 — Living data (Dynamic Fuel State)

> *A twin that reads the territory as it is today — static fuel maps go stale the moment they are drawn. A living fuel layer is the single biggest accuracy gain available to the fire model.*

| Direction | Horizon | Why it's interesting |
|---|---|---|
| ★ **Dynamic NDVI → Dynamic Fuel State** | Now | Turn satellite "greenness" (NDVI) into a live fuel-moisture and fuel-state layer, so the simulator burns *today's* fuel. The NDVI pipeline already exists. |
| Always-current fuels | Next | Burn scars, drought stress, harvests and regrowth update the fuel map automatically from each new satellite pass — and flag stressed, fire-prone vegetation weeks ahead. |

### Pillar 3 — Intelligence that learns and sips energy

> *More capable does not have to mean more power-hungry. The goal is intelligence that learns from every fire, always under human oversight, while using less energy each year.*

| Direction | Horizon | Why it's interesting |
|---|---|---|
| Agentic assistance | Next | Software agents that draft the morning risk briefing, surface anomalies and propose interventions — always presented for a human to approve, never acting unsupervised. |
| ★ **Frugal & green AI** | Next | Smaller, distilled models and inference at the edge — closer to the sensors — for lower energy, lower cost and resilience when connectivity drops. Sustainability built into the AI itself, not just the forest. |
| Self-learning & self-improvement | Later | The platform calibrates itself against what really happened — every fire it predicted well or badly becomes training signal. Needs careful governance. |

### Pillar 4 — A platform to build on

> *The real prize is a modular platform — composable building blocks that let a twin or a decision-support tool be assembled for a new territory, a new hazard or a new audience, instead of rebuilt from scratch each time.*

| Direction | Horizon | Why it's interesting |
|---|---|---|
| A "Lego bricks" architecture | Next | Reusable bricks — a hazard model, a data feed, a map layer, a report — that snap together. Stand up a new twin by composing parts that are already tested. |
| ★ **Decision support for new sectors** | Next | A DST tuned for **insurers** (risk pricing + portfolio exposure), **infrastructure operators** (network resilience) and **spatial / urban planners** (risk-aware planning). New audiences for the same evidence base. |
| Plug-in interconnection | Next | Open APIs and connectors so the twin talks to GIS, emergency-management, environmental and IoT systems — one holistic cockpit, not another silo. |
| Regenerative engineering | Later | Aim beyond resisting hazard toward restoring it: nature-based, net-positive interventions. The twin becomes a design tool for regeneration, not only defence. |

### Pillar 5 — Scale

> *The cross-border Karst is the proving ground. The same engine grows outward in deliberate steps — each one mostly data and compute, the science already in place.*

| Step | Horizon |
|---|---|
| **01 — All Friuli-Venezia Giulia** | Now |
| **02 — All of Slovenia** | Now → Next |
| **03 — The Mediterranean** | Later — the climate-and-fire frontline; a shared twin for a shared sea |

### Now · Next · Later

| Horizon 1 — Now (0–12 mo) | Horizon 2 — Next (1–2 yr) | Horizon 3 — Later (2–4 yr) |
|---|---|---|
| Dynamic Fuel State (NDVI) layer | Compound / multi-risk index | Seismic correlation in the compound index |
| Flood & extreme-heat hazard layers | Agentic assistance + frugal AI | Self-improving autonomy (governed) |
| Scale to all FVG & Slovenia | Modular DST for insurers & infrastructure | Regenerative-engineering design suite |
|  | Plug-in / API ecosystem | A Mediterranean-wide twin |

### Where we'd start

Three things to build first — highest impact, least new plumbing:

1. **The Dynamic Fuel State layer** *(now)* — shovel-ready, the NDVI pipeline already feeds the platform; sharpens every fire forecast for the least new effort.
2. **Flood & extreme-heat layers** *(now)* — the fastest way to become multi-hazard; reuses the existing weather network + 3D terrain.
3. **Scale to all FVG & Slovenia** *(now)* — mostly data and compute, little new science; multiplies the platform's reach before the harder leap to the Mediterranean.

Everything else — compound multi-risk, agentic & frugal AI, the modular decision-support platform, the Mediterranean twin — builds on these three foundations.

---

## Principles — what holds across every step

- **Frugal & green by design** — less energy, less cost. Efficiency is a feature, not an afterthought.
- **Human-in-the-loop** — AI proposes; people decide. Automation assists, it never acts alone.
- **Open & modular** — composable bricks and open interfaces, so others can build on the work.
- **Cross-border & shared** — hazards ignore borders; the data and the tools should too.
- **Regenerative, not just protective** — leave the territory and its communities stronger than we found them.
- **Privacy & transparency** — anonymised by default, methods explained, results open to scrutiny.

---

## First deployment: Karst Firewall 5.0

TerraWise's first full deployment is the **EU Interreg Italy–Slovenia VI-A** project *Karst Firewall 5.0* (2024–2027). Public Interreg-facing documentation lives in [`infordata-sistemi/karst-firewall-50`](https://github.com/infordata-sistemi/karst-firewall-50). The public portal is online at [karst-map.way.to.it/portal](https://karst-map.way.to.it/portal).

---

## Modules

The implementation is split across a family of repositories. See [MODULES.md](MODULES.md) for the canonical index; the headline ones:

| Repo | Role |
|---|---|
| [`kf50-php`](https://github.com/infordata-sistemi/kf50-php) | Operator cockpit + public portal (Yii2 / PHP) |
| [`kf50-observation-ingest`](https://github.com/infordata-sistemi/kf50-observation-ingest) | Ingest pipeline: gateways → Influx (primary) + MySQL (fallback) |
| [`kf50-sensors`](https://github.com/infordata-sistemi/kf50-sensors) | IoT sensor + LoRaMIP gateway firmware / configuration |
| [`kf50-kfwi-api`](https://github.com/infordata-sistemi/kf50-kfwi-api) | Karst Fire Weather Index ML service |
| [`kf50-seneh_ml`](https://github.com/infordata-sistemi/kf50-seneh_ml) | Sensor-network e-nose ML classification |
| [`kf50-dji-bridge`](https://github.com/infordata-sistemi/kf50-dji-bridge) | DJI drone + dock read-only ingest service |
| [`kf50-osrm`](https://github.com/infordata-sistemi/kf50-osrm) | Self-hosted OSRM routing for intervention dispatch |
| [PyroWISE engine](https://github.com/markopetelin/infordata-kf50-firegrowth) | Fire-spread simulator core + GIS layer provider |

PyroWISE's open scientific documentation has its own home at [`infordata-sistemi/pyrowise`](https://github.com/infordata-sistemi/pyrowise).

---

## Architecture at a glance

See [ARCHITECTURE.md](ARCHITECTURE.md) for the full data-flow and component diagram. The short version:

```
 ┌──────────────┐   ┌────────────────────┐   ┌──────────────┐
 │ field assets │   │ kf50-observation-  │   │  InfluxDB    │
 │ (sensors,    │──▶│ ingest             │──▶│  (primary)   │
 │  gateways,   │   │ (validate · route) │   │              │
 │  drones)     │   │                    │   ├──────────────┤
 └──────────────┘   └─────────┬──────────┘   │  MySQL       │
                              │              │  (inventory  │
                              │              │   + fallback)│
                              ▼              └──────────────┘
                      ┌────────────────┐              │
                      │  kf50-kfwi-api │              │
                      │  · ignition ML │              ▼
                      │  · FWI calibr. │      ┌────────────────┐
                      └────────┬───────┘      │  kf50-php      │
                               │              │  · cockpit     │
                               └─────────────▶│  · public      │
                                              │    portal      │
                  PyroWISE  ───────────────▶  │  · alerting    │
                  firegrowth                  └────────────────┘
```

---

## Status

- **Karst Firewall 5.0 (Interreg)** — running pilot. ~90% project progress; closes 14 August 2026.
- **TerraWise as a product** — Karst is the reference deployment; the architecture is being prepared for a second site.
- **This repo** — seeded; documentation roll-out is in progress. See [ROADMAP.md](ROADMAP.md) for the full living roadmap.

---

## Licensing

This umbrella documentation is licensed under [CC BY 4.0](LICENSE). The underlying modules each follow their own licence — see each repo for details. Karst Firewall 5.0 follows an open-core model:

- **Core community platform** — EUPL-1.2-or-later (open source).
- **Documentation, methodology & datasets** — CC BY 4.0.
- **Advanced modules & SaaS** — proprietary, commercial.

The PyroWISE simulation engine has an explicit open-vs-commercial boundary at [`infordata-sistemi/pyrowise/OPEN_VS_COMMERCIAL.md`](https://github.com/infordata-sistemi/pyrowise/blob/main/OPEN_VS_COMMERCIAL.md).

---

## Get involved

The roadmap above is **open to partners**. If you're an insurer, infrastructure operator, municipality, planner, civil-protection agency or researcher and one of these directions matters to you, tell us — we'd rather build the next pillar with you than for you.

### Contact

- **Product (commercial · partnerships · SaaS)** — `sales@infordata.it`
- **Karst Firewall 5.0 (project coordination, IUAV)** — `karstfirewall@iuav.it`
- **Open development** — file an issue on the relevant module repo.

---

*Co-funded by the Interreg VI-A Italy–Slovenia Programme · Project ITA-SI0600146 · 2024–2027.*
