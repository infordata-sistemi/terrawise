# TerraWise modules

This is the canonical index of the repositories that make up the TerraWise platform. Each module has a single, sharp role; together they form the four-pillar capability (Warning · Intelligence · Simulation · Evaluation).

## Application + portal

| Repo | Stack | Role |
|---|---|---|
| [`kf50-php`](https://github.com/infordata-sistemi/kf50-php) | PHP 8 · Yii2 · MySQL | The operational cockpit for civil-protection teams and the public portal. Houses the alerting engine, the live-risk map, the 3D twin, the simulator UI and the multi-language content (IT / SL / EN / DE). |

## Data plane

| Repo | Stack | Role |
|---|---|---|
| [`kf50-observation-ingest`](https://github.com/infordata-sistemi/kf50-observation-ingest) | Python · FastAPI · InfluxDB · MySQL | The ingest pipeline. Validates, deduplicates and routes every observation (weather stations, IoT sensors, gateway heartbeats) into Influx (primary time-series store) and karst MySQL (inventory + fallback sink). |
| [`kf50-sensors`](https://github.com/infordata-sistemi/kf50-sensors) | LoRa · embedded | IoT sensor and LoRaMIP gateway firmware + provisioning. The BME688 e-nose nodes, the LoRaWAN backbone, and the gateway-side config. |
| [`kf50-dji-bridge`](https://github.com/infordata-sistemi/kf50-dji-bridge) | Python · DJI SDK | Read-only ingest of DJI drone and dock telemetry into the platform (`WI-F`). |

## Intelligence

| Repo | Stack | Role |
|---|---|---|
| [`kf50-kfwi-api`](https://github.com/infordata-sistemi/kf50-kfwi-api) | Python · scikit-learn | The Karst Fire Weather Index service: Karst-calibrated FWI severity + a Random Forest ignition model (AUC 0.934, 77.5% detection). |
| [`kf50-seneh_ml`](https://github.com/infordata-sistemi/kf50-seneh_ml) | Python · ML | Sensor-network e-nose ML — classifies VOC signatures of early combustion against background air. |

## Simulation

| Repo | Stack | Role |
|---|---|---|
| [PyroWISE firegrowth engine](https://github.com/markopetelin/infordata-kf50-firegrowth) | C++ / Python | The fire-spread simulator core, the GIS layer provider, and the Huygens-wavefront / Rothermel-surface model implementation. **Open scientific documentation:** [`infordata-sistemi/pyrowise`](https://github.com/infordata-sistemi/pyrowise). |

## Routing & dispatch

| Repo | Stack | Role |
|---|---|---|
| [`kf50-osrm`](https://github.com/infordata-sistemi/kf50-osrm) | OSRM · Docker | Self-hosted OSRM routing for cross-border intervention dispatch (FVG + Slovenia). |

## Documentation

| Repo | Audience | Role |
|---|---|---|
| [`terrawise`](https://github.com/infordata-sistemi/terrawise) **(this repo)** | Customers · evaluators · partners | The product umbrella — architecture, module index, roadmap. |
| [`karst-firewall-50`](https://github.com/infordata-sistemi/karst-firewall-50) | Citizens · Interreg programme · municipalities | Public Interreg-facing project documentation. |
| [`pyrowise`](https://github.com/infordata-sistemi/pyrowise) | Scientific community · academic citers | Open scientific documentation for the PyroWISE simulation engine. |

---

## How they fit together

See [ARCHITECTURE.md](ARCHITECTURE.md) for the data-flow diagram and the cross-module integration contracts.
