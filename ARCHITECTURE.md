# TerraWise architecture

> **Status:** initial seed. Diagrams and integration contracts are being lifted out of the operational repos as this document evolves. PRs welcome.

## Design principles

1. **Influx is the source of truth for time-series.** MySQL is a fallback sink + the inventory store, not a parallel mirror.
2. **Single-direction data flow.** Field assets → ingest → storage → API → UI. No back-channels.
3. **Module replaceability over coupling.** Each module exposes a stable HTTP / message contract; internals can be rewritten independently.
4. **Operational + public surfaces are separated.** The cockpit (login-gated) and the public portal share the same data plane but never the same routes.
5. **Multi-language at the edge.** All citizen-facing strings flow through the `Portal` i18n category (IT / SL / EN / DE).
6. **Hazard context is consumed, never injected.** The multi-hazard layer (TerraWise) feeds the cockpit and run-provenance, but never the fire-spread physics — enforced by an import-lint boundary, not just convention.

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

## TerraWise multi-hazard layer — data, not code

PyroWISE is the wildfire engine; **TerraWise** is a sibling **multi-hazard data/event layer** (earthquake · flood / hydro · heatwave · warnings), shipped as an opt-in, flag-gated preview. The two never share code — the contract between them, and out to the cockpit, is **data**.

```
 external hazard sources           TerraWise — data-only layer            consumer
 ─────────────────────────         ───────────────────────────           ────────────
 INGV · EMSC · USGS                 ingest adapters → dedup                kf50-php
 ARSO · FVG · ISPRA ·       ──────▶  → exposure summary           ──────▶  TerraWise
 Copernicus EMS                     → STAC + MinIO products                dashboard
 MeteoAlarm · ERA5-HEAT             (GeoJSON/GeoParquet/COG/Zarr;          (read-only)
                                    layers.json + manifest.json)
                                    → read-only  /terrawise/*  API

         (provenance only — consumed, never injected; NO physics coupling)
                                    │
                                    ▼
                          PyroWISE wildfire engine
                          manifest.terrawise_context  (additive, default OFF)
```

**The boundary (non-negotiable).** TerraWise must not touch the fire-spread physics. It lives as a data-only package and **may not import the wildfire kernels** — an AST-lint test fails the build if it tries. The only coupling back to PyroWISE is the additive `manifest.terrawise_context` provenance block (default OFF), which records *which* hazard events a run considered; it never changes the simulation. A heatwave/wind event MAY *trigger* a scenario run, but only an operator (or orchestrator) decides — TerraWise just emits the event.

**The integration contract is data, not code.** Products are published to **MinIO** with a **STAC 1.0** item, a deterministic `manifest.json` (sha256, source, license, CRS, quality flags, fallback status) and a `layers.json` index, in the same materialisations PyroWISE already uses (GeoJSON / GeoParquet / GPKG / COG / Zarr). The cockpit consumes them over **stable HTTP + MinIO URLs only** — no PHP→Python, no Python→PHP.

**Read-only HTTP surface** — `/terrawise/*`, gated by `PYROWISE_TERRAWISE_API_ENABLED` (dark by default); same `X-PyroWISE-Internal-Key` auth as `/runs/*`, except `/terrawise/health`, which is open:

| Endpoint | Returns |
|---|---|
| `GET /terrawise/aoi/{aoi_profile_id}/layers` | the hazard-layer catalogue for an AOI |
| `GET /terrawise/events` | hazard events, filterable by `hazard_type` · `bbox` · `since` / `until` |
| `GET /terrawise/events/{event_id}` | one canonical event |
| `GET /terrawise/exposure-summary?event_id=…` | aggregate (no-PII) exposure for an event |
| `GET /terrawise/sources` | declarative provider / license / cadence registry |
| `GET /terrawise/health` | adapter liveness (unauthenticated) |

**AOI profiles & CRS discipline.** Each Area of Interest is a versioned profile (`karst_itaslo_v1`, `fvg_v1`, `slovenia_v1`) declaring its sources, licenses and CRS. CRS is explicit at every hop: **raw** source CRS → **canonical** AOI CRS (EPSG:3794 for Karst) → **web** publication CRS (EPSG:4326). No site-specific calibration transfers between AOIs without evidence.

**Cockpit layer groups.** The Karst operator dashboard organises TerraWise into five groups — **live events** · **warnings** · **hazard zones** · **exposure & vulnerability** · **scenario outputs**. Public vs operational surfaces are RBAC-separated (contacts and sensitive infrastructure are operational-only), and all strings flow through the four-language `Terrawise` i18n category (IT / SL / EN / DE).

## Sections to expand

- [ ] Per-module API contracts (OpenAPI / message schemas)
- [ ] Authentication topology (internal-key bypass, RBAC for cockpit)
- [ ] Storage retention policies (Influx down-sampling, MySQL archival)
- [ ] Deployment topology (production karst-map.way.to.it stack)
- [ ] Disaster-recovery + degradation modes (what stays alive when X is down)
- [ ] Integration-test matrix (which contracts are end-to-end covered)
- [ ] TerraWise integration contract (the `/terrawise/*` schemas, the STAC / MinIO product layout, the AOI-profile registry)

Open an issue or PR if a section is blocking work.
