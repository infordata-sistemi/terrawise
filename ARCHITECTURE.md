# TerraWise architecture

> **Status:** initial seed. Diagrams and integration contracts are being lifted out of the operational repos as this document evolves. PRs welcome.

## Design principles

1. **Influx is the source of truth for time-series.** MySQL is a fallback sink + the inventory store, not a parallel mirror.
2. **Single-direction data flow.** Field assets → ingest → storage → API → UI. No back-channels.
3. **Module replaceability over coupling.** Each module exposes a stable HTTP / message contract; internals can be rewritten independently.
4. **Operational + public surfaces are separated.** The cockpit (login-gated) and the public portal share the same data plane but never the same routes.
5. **Multi-language at the edge.** All citizen-facing strings flow through the `Portal` i18n category (IT / SL / EN / DE).

## High-level data flow

```
 ┌──────────────┐   ┌────────────────────┐   ┌──────────────┐
 │ field assets │   │ kf50-observation-  │   │  InfluxDB    │
 │ · weather    │   │ ingest             │──▶│  (primary    │
 │   stations   │──▶│ · validate         │   │   time-      │
 │ · IoT e-nose │   │ · deduplicate      │   │   series)    │
 │ · LoRaMIP    │   │ · route            │   │              │
 │   gateways   │   │ · enrich           │   ├──────────────┤
 │ · drones     │   │                    │──▶│  MySQL       │
 └──────────────┘   └─────────┬──────────┘   │  · inventory │
                              │              │  · fallback  │
                              ▼              └──────┬───────┘
                      ┌────────────────┐            │
                      │  kf50-kfwi-api │◀───────────┘
                      │  · ignition ML │
                      │  · FWI calibr. │
                      └────────┬───────┘
                               │
                               ▼
                      ┌────────────────┐    ┌──────────────────┐
                      │   kf50-php     │◀───│ PyroWISE         │
                      │ · cockpit      │    │ firegrowth (sim) │
                      │ · public portal│    └──────────────────┘
                      │ · alerting     │
                      │ · 3D twin      │
                      └────────┬───────┘
                               │
                               ▼
                      civil-protection ops + citizens
```

## Sections to expand

- [ ] Per-module API contracts (OpenAPI / message schemas)
- [ ] Authentication topology (internal-key bypass, RBAC for cockpit)
- [ ] Storage retention policies (Influx down-sampling, MySQL archival)
- [ ] Deployment topology (production karst-map.way.to.it stack)
- [ ] Disaster-recovery + degradation modes (what stays alive when X is down)
- [ ] Integration-test matrix (which contracts are end-to-end covered)

Open an issue or PR if a section is blocking work.
