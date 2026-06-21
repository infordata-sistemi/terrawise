# Changelog

All notable changes to TerraWise public documentation are tracked here.

## 2026-06-20 — Platform-delta sync: TerraWise multi-hazard (opt-in preview)

The multi-hazard pillar has reached the platform as an **opt-in, flag-gated preview** — the second pillar (after Dynamic Fuel State) to move from roadmap to shipped. PyroWISE stays the wildfire engine; **TerraWise** is the new multi-hazard data/event layer. Hazard context is *consumed, never injected* — it never alters the fire-spread physics.

**Engine side (PyroWISE repo — `WI-TERRAWISE-KARST-MULTIHAZARD`, P0–P3 shipped):**

- **Multi-hazard ingest layer.** A data-only `terrawise/` package with nine wired ingest adapters — earthquake (USGS, INGV, EMSC), flood / hydro (ARSO hydro, FVG Civil Protection, ISPRA IdroGEO, Copernicus EMS) and heatwave (MeteoAlarm, ERA5-HEAT) — plus cross-source de-duplication, an aggregate (no-PII) exposure summariser, and a STAC + MinIO product publisher.
- **Read-only `/terrawise/*` HTTP API** (six endpoints: AOI layer catalogue, events, event detail, exposure-summary, sources, health). **Dark by default** — gated behind `PYROWISE_TERRAWISE_API_ENABLED`; a Karst-only deployment is unaffected.
- **Data-not-code boundary, enforced.** TerraWise may not import the wildfire kernels (an AST-lint test fails the build otherwise); the additive `manifest.terrawise_context` block is **provenance-only** and never feeds the physics.

**Frontend side (`kf50-php` — `WI-DASHBOARD-TERRAWISE-V1` shipped):**

- A **read-only operator dashboard** (`/terra-wise`) surfacing the hazard-layer catalogue, a filterable event browser (hazard type · time window · bbox), source provenance and adapter health — built on RBAC (public / operational / planning scopes) and four-language i18n (IT · SL · EN · DE). It consumes the engine over HTTP + MinIO URLs only and falls back to local stub data when the flag is off or the API is unreachable.

**Honest scope.** This is a preview: the API is off by default, the OGS earthquake source is still *planned* (endpoint-stability gating), population-exposure estimates are not yet available, and the operator panel serves fallback data until the flag is enabled. Compound / multi-risk fusion across hazards remains a *Next* item.

## 2026-06-14 — Platform-delta sync

Documentation synced with the latest improvements shipped in `kf50-php` and the PyroWISE engine:

- **Dynamic Fuel State — first opt-in preview.** Documented across README + ROADMAP (Pillar 2): PyroWISE now assimilates a per-fuel-class NDVI anomaly into a bounded per-class rate-of-spread modulation, exposed as an opt-in simulator toggle (off by default, provenance-tagged), gated behind an A/B hindcast against the static-fuel baseline. The "living data" pillar is no longer only a roadmap line.
- **Agentic layer — seventh assistant.** Noted the new *active-fire trigger* (clusters FIRMS detections, proposes a nowcast per cluster for operator review; propose-only).
- **Ensemble rendering.** Simulator now renders a burn-probability surface + p10/p50/p90 arrival envelopes.
- **Accuracy fix.** `MODULES.md` — PyroWISE engine stack corrected to *Python · FastAPI* (pure-Python clean-room reimplementation), matching the PyroWISE README.

## Unreleased

- Initial seed: README, MODULES index, ARCHITECTURE skeleton, ROADMAP.
- Established the umbrella → first-deployment (Karst Firewall 5.0) → simulation-engine (PyroWISE) docs structure.
