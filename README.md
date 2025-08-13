# Cisco-VIP-2025-Networking-Tool

This tool parses router/switch configs to auto-generate a hierarchical network topology, validates configs,
analyzes capacity vs. traffic, and simulates Day‑1 discovery and Day‑2 fault injection.

## Quickstart

```bash
# 1) Create and activate a virtual environment (recommended)
python -m venv .venv && source .venv/bin/activate  # (Linux/macOS)
# On Windows: .venv\Scripts\activate

# 2) Install requirements
pip install -r requirements.txt

# 3) Run the CLI help
python -m netgen.cli --help

# 4) Parse sample configs
python -m netgen.cli parse examples/Conf --out build/parsed.json

# 5) Build topology + interactive HTML
python -m netgen.cli topo build/parsed.json --viz build/topology.html

# 6) Validate for common issues
python -m netgen.cli validate build/parsed.json --policy policy/policy.yaml --out build/findings.json

# 7) Capacity plan (stub logic)
python -m netgen.cli plan build/topology.json --traffic examples/traffic_profile.yaml --out build/plan.json

# 8) Day-1 simulation (stub)
python -m netgen.cli simulate build/topology.json --events examples/scenarios_day1.yaml --out build/sim
```

Artifacts will appear in the `build/` directory.

## Project Layout

```
src/netgen            # package
  parse/              # config parsers
  model/              # data models
  topo/               # topology inference & viz
  validate/           # rules
  plan/               # capacity & LB
  sim/                # simulation (threads/IPC stubs)
  ipc/                # IPC channels stubs
examples/             # sample configs, traffic, scenarios
policy/               # default validation thresholds
build/                # generated outputs
```

## Notes
- Minimal working stubs are provided so the CLI runs end-to-end.
- You can extend parsing templates and rules as needed.
