# TerraWise

> **T**erritorial **E**mergency **R**isk & **R**esilience **A**nalytics — **W**arning, **I**ntelligence, **S**imulation & **E**valuation.

TerraWise is **Infordata Sistemi**'s territorial-emergency platform: a digital twin that pairs live risk monitoring, AI-driven warning and fire-spread simulation to help authorities prevent, anticipate and respond to wildfires and adjacent territorial emergencies.

This repository is the **public umbrella** — what TerraWise is, how the modules fit together, where to find each one, and where the project is going. The implementation lives in the family of `kf50-*` repositories (see [MODULES.md](MODULES.md)).

---

## The four capabilities

| Pillar | What it does | Today in production |
|---|---|---|
| **Warning** | Detect early signals — VOC e-noses, thermal IR cameras, satellites, citizen reports — and turn them into prioritised alerts | Karst Firewall 5.0 operational cockpit · alerting via email / SMS / WhatsApp |
| **Intelligence** | Score risk at street level by fusing Karst-calibrated fire-weather (FWI) and a machine-learning ignition model | KFWI: **77.5%** fire detection vs **29%** baseline; ignition model AUC **0.934** |
| **Simulation** | Forward-simulate fire spread on the live digital twin — Huygens propagation over a Rothermel surface-fire model | PyroWISE engine; nowcasts on demand and pre-computed scenarios |
| **Evaluation** | Compare forecasts to outcomes; validate prevention investments with measurable evidence | Post-incident IoU against observed perimeters; 30-year burned-area baseline (Sentinel/Landsat) |

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
- **This repo** — seeded. Documentation roll-out is in progress; see [ROADMAP.md](ROADMAP.md).

---

## Licensing

This umbrella documentation is licensed under [CC BY 4.0](LICENSE). The underlying modules each follow their own licence — see each repo for details. Karst Firewall 5.0 follows an open-core model:

- **Core community platform** — EUPL-1.2-or-later (open source).
- **Documentation, methodology & datasets** — CC BY 4.0.
- **Advanced modules & SaaS** — proprietary, commercial.

---

## Contact

- **Product (commercial · partnerships · SaaS)** — `sales@infordata.it`
- **Karst Firewall 5.0 (project coordination, IUAV)** — `karstfirewall@iuav.it`
- **Open development** — file an issue on the relevant module repo.

---

*Co-funded by the Interreg VI-A Italy–Slovenia Programme · Project ITA-SI0600146 · 2024–2027.*
