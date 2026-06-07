# TerraWise roadmap

> The product roadmap, openly shared. Internal coordination and sprint planning live elsewhere; this file is what we're comfortable saying out loud about direction. The most accessible, multilingual version is at [karst-map.way.to.it/portal/roadmap](https://karst-map.way.to.it/portal/roadmap) (IT · SL · EN · DE) — this file mirrors it for engineering audiences.

---

## Why this roadmap exists

Today, TerraWise (deployed as **Karst Firewall 5.0**) is a cross-border wildfire twin. This is where we want to take it next: a **living, multi-hazard decision platform** that learns, sips energy, scales from the Karst to the whole Mediterranean, and gives insurers, infrastructure operators and planners modular tools to build on.

> ⚠ **None of the directions below are live yet.** This is the direction we are taking the platform, openly and with our partners.

Four shifts shape everything:

1. **From a single hazard (fire) to many** — flood, heat, slope, seismic, compound.
2. **From static maps to living data** — the twin reads the territory as it is *today*, not last season.
3. **From a finished tool to a modular platform** — composable bricks others can build on.
4. **From one plateau to a sea** — the Karst is the proving ground; the Mediterranean is the ambition.

---

## Where we'd start — recommended first moves

Highest impact, least new plumbing.

| # | Direction | Why first |
|---|---|---|
| 01 · Now | **Dynamic Fuel State (NDVI) layer** | Shovel-ready: the satellite NDVI / vegetation-health pipeline already feeds the platform. Turning it into a live "how dry is the fuel today" layer sharpens every fire forecast for the least new effort — the clearest win. |
| 02 · Now | **Flood & extreme-heat layers** | The fastest way to become multi-hazard: the cross-border weather network and 3D terrain we already run are most of what flood and heat-wave mapping needs. Two hazards that touch every citizen — not only fire crews. |
| 03 · Now | **Scale to all FVG & Slovenia** | Mostly data and compute, little new science. Covering the whole region multiplies the platform's reach and value before the harder leap to the wider Mediterranean. |

Everything else — compound multi-risk, agentic & frugal AI, the modular decision-support platform, the Mediterranean twin — builds on these three foundations.

---

## Pillar 1 — Multi-hazard

> *From a wildfire twin to a multi-hazard twin.* The Karst does not face only fire. The same living twin — terrain, weather, exposure — can read flood, heat, slope and seismic risk, and, crucially, where they overlap on the same people and assets.

| Direction | Horizon | Impact |
|---|---|---|
| ★ **Flooding & flash floods** | Now | High · reuses the weather network + 3D terrain |
| ★ **Extreme heat & "heat bombs"** | Now | High · directly serves citizens & health services |
| Slope instability & landslides | Next | Medium · compounds with fire & flood |
| Seismic & compound risk | Next | High · the multi-hazard payoff — one compound-risk index, not four maps read in isolation |

**Flooding & flash floods.** Pluvial and flash-flood exposure from rainfall, terrain hydrology and the karstic underground drainage — where water gathers fast on the limestone, and which roads, homes and assets sit in its path.

**Extreme heat & "heat bombs".** Heat-wave and urban-heat exposure from the station network and land cover — a public-health early warning for the most vulnerable people and places, *and* a fuel-drying signal that feeds the fire model.

**Slope instability & landslides.** Landslide susceptibility from slope, soil and rainfall — sharpened *after* fires, when burnt ground sheds water and the risk of debris flows climbs. A natural pairing with the post-fire recovery view.

**Seismic & compound risk.** Overlay seismic hazard and cross-correlate the layers: where do fire, flood, heat and earthquake stack on the same zone? Compound exposure is what planning and insurance really need.

---

## Pillar 2 — Living data (Dynamic Fuel State)

> *A twin that reads the territory as it is today.* Static fuel maps go stale the moment they are drawn. Reading vegetation from space, continuously, makes the twin's fuel "alive" — and a living fuel layer is the single biggest accuracy gain available to the fire model.

| Direction | Horizon | Impact |
|---|---|---|
| ★ **Dynamic NDVI → Dynamic Fuel State** | Now | High · the NDVI pipeline already exists |
| Always-current fuels | Next | Medium · keeps every hazard model honest |

**Dynamic NDVI → Dynamic Fuel State.** Turn the satellite "greenness" (NDVI) signal into a live fuel-moisture and fuel-state layer, so the fuel the simulator burns is *today's* fuel — green and damp, or cured and flammable — not last season's static map.

**Always-current fuels.** Burn scars, drought stress, harvests and regrowth update the fuel map automatically from each new satellite pass — and flag stressed, fire-prone vegetation weeks ahead, turning the twin into an early-warning instrument for the land itself.

---

## Pillar 3 — Intelligence that learns and sips energy

> *More capable does not have to mean more power-hungry.* The platform should get better on its own, and do so frugally — learning from every fire, always under human oversight, while using less energy each year.

| Direction | Horizon | Impact |
|---|---|---|
| Agentic assistance | Next | High · saves operators time daily |
| ★ **Frugal & green AI** | Next | High · cuts running cost & carbon |
| Self-learning & self-improvement | Later | High · but needs careful governance |

**Agentic assistance.** Software agents that watch the live data, draft the morning risk briefing, surface anomalies and propose interventions — always presented for a human to approve, never acting unsupervised. *(A first instance ships today on Karst Firewall 5.0 — see the [PyroTwin agentic layer](https://github.com/infordata-sistemi/karst-firewall-50#agentic-features--pyrotwin-operator-assistants).)*

**Frugal & green AI.** Smaller, distilled models and inference at the edge — closer to the sensors — for lower energy, lower cost and resilience when connectivity drops. Sustainability built into the AI itself, not just into the forest.

**Self-learning & self-improvement.** Close the loop: the platform calibrates itself against what really happened — every fire it predicted well or badly becomes training signal — so accuracy improves over time without a manual rebuild.

---

## Pillar 4 — A platform to build on

> *The real prize is a modular platform.* Composable building blocks that let a twin or a decision-support tool be assembled for a new territory, a new hazard or a new audience — instead of rebuilt from scratch each time.

| Direction | Horizon | Impact |
|---|---|---|
| A "Lego bricks" architecture | Next | High · multiplies everything else |
| ★ **Decision support for new sectors** | Next | High · opens a sustainable business model |
| Plug-in interconnection | Next | Medium · the glue for an ecosystem |
| Regenerative engineering | Later | Strategic · the long-term ethos |

**A "Lego bricks" architecture.** Reusable bricks — a hazard model, a data feed, a map layer, a report — that snap together. Stand up a new digital twin by composing parts that are already tested, not by writing it all again.

**Decision support for new sectors.** A decision-support tool (DST) tuned for **insurers** (risk pricing + portfolio exposure), **infrastructure operators** (network resilience) and **spatial / urban planners** (risk-aware planning). New audiences for the same evidence base.

**Plug-in interconnection.** Open APIs and connectors so the twin talks to GIS, emergency-management, environmental and IoT systems — one holistic cockpit for managing territorial sustainability, rather than another silo.

**Regenerative engineering.** Aim beyond *resisting* hazard toward *restoring* it: nature-based, net-positive interventions that leave ecosystems and communities stronger than before. The twin becomes a design tool for regeneration, not only defence.

---

## Pillar 5 — Scale

> *The cross-border Karst is the proving ground.* The same engine can grow outward in deliberate steps — each one mostly data and compute, the science already in place.

| Step | Horizon | What it means |
|---|---|---|
| **01 — All Friuli-Venezia Giulia** | Now | The natural next catchment, with regional data partners already in place. |
| **02 — All of Slovenia** | Now → Next | A truly national, cross-border twin — completing the picture for the whole Slovenian side, not just the border strip. |
| **03 — The Mediterranean** | Later | The climate-and-fire frontline. A shared twin for a shared sea — the ambition that gives every brick above its full meaning. |

---

## Now · Next · Later (the sequence)

The same initiatives, sequenced by impact and readiness. Our honest view of the order — not a contract, but where the leverage is.

| Horizon 1 — Now (0–12 mo) | Horizon 2 — Next (1–2 yr) | Horizon 3 — Later (2–4 yr) |
|---|---|---|
| Dynamic Fuel State (NDVI) layer | Compound / multi-risk index | Seismic correlation in the compound index |
| Flood & extreme-heat hazard layers | Agentic assistance + frugal AI | Self-improving autonomy (governed) |
| Scale to all FVG & Slovenia | Modular DST for insurers & infrastructure | Regenerative-engineering design suite |
|  | Plug-in / API ecosystem | A Mediterranean-wide twin |

---

## Principles — what holds across every step

- **Frugal & green by design** — less energy, less cost. Efficiency is a feature, not an afterthought.
- **Human-in-the-loop** — AI proposes; people decide. Automation assists, it never acts alone.
- **Open & modular** — composable bricks and open interfaces, so others can build on the work.
- **Cross-border & shared** — hazards ignore borders; the data and the tools should too.
- **Regenerative, not just protective** — leave the territory and its communities stronger than we found them.
- **Privacy & transparency** — anonymised by default, methods explained, results open to scrutiny.

---

## Help shape the roadmap

The directions above are **open to partners**. If you are:

- an **insurer** (risk pricing, portfolio exposure, claims),
- an **infrastructure operator** (utilities, transport, telecoms — network resilience under multi-hazard stress),
- a **municipality** or a **planning authority**,
- a **civil-protection** agency, or
- a **researcher** working on any of the pillars above,

…tell us which challenge matters most to you. We'd rather build the next pillar *with* you than *for* you.

- **Open the conversation** — `sales@infordata.it`
- **File an issue** on this repo to discuss a specific direction publicly.
- **See the platform live** at [karst-map.way.to.it/portal](https://karst-map.way.to.it/portal).

---

*Last updated alongside the [portal roadmap](https://karst-map.way.to.it/portal/roadmap). This is a rolling document — open an issue if you'd like to discuss timing or dependencies.*
