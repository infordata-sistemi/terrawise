# Changelog

All notable changes to TerraWise public documentation are tracked here.

## 2026-06-14 — Platform-delta sync

Documentation synced with the latest improvements shipped in `kf50-php` and the PyroWISE engine:

- **Dynamic Fuel State — first opt-in preview.** Documented across README + ROADMAP (Pillar 2): PyroWISE now assimilates a per-fuel-class NDVI anomaly into a bounded per-class rate-of-spread modulation, exposed as an opt-in simulator toggle (off by default, provenance-tagged), gated behind an A/B hindcast against the static-fuel baseline. The "living data" pillar is no longer only a roadmap line.
- **Agentic layer — seventh assistant.** Noted the new *active-fire trigger* (clusters FIRMS detections, proposes a nowcast per cluster for operator review; propose-only).
- **Ensemble rendering.** Simulator now renders a burn-probability surface + p10/p50/p90 arrival envelopes.
- **Accuracy fix.** `MODULES.md` — PyroWISE engine stack corrected to *Python · FastAPI* (pure-Python clean-room reimplementation), matching the PyroWISE README.

## Unreleased

- Initial seed: README, MODULES index, ARCHITECTURE skeleton, ROADMAP.
- Established the umbrella → first-deployment (Karst Firewall 5.0) → simulation-engine (PyroWISE) docs structure.
