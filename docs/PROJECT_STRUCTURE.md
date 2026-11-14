# Project organization

`README.md` is the entry point. `reports/NEXT_STEPS.md` records completed work and
the outstanding case-study inputs. The original handoff is preserved verbatim in
`rooftops_repowered_v2_context.txt`; newer explicit user decisions and the current
configuration supersede its older artifact paths and pending statuses.

```text
config/
  project.json                    # paths, selected demand route, deferred host
  simulation.json                 # office operation grid, weather-year convention
  impact_assumptions.json          # intentionally unset sourced costs/carbon
  experiments/                    # initial benchmark protocol and excluded test IDs
pipeline/
  __main__.py                     # command-line entry point
  common.py, temporal.py          # shared validation/config/time helpers
  data_audit/                     # source scans and quality reports
  demand_preparation/             # measured cohort, features, train/validation/test
  demand_baseline_hour_of_week/   # reference estimator
  demand_baseline_seasonal/       # reference estimator
  demand_xgboost/                 # measured-data benchmark and inference
  simulation_surrogate/           # EnergyPlus setup, scenarios, training, inference
  pvgis/                          # generation import, no new PV physics
  scenarios/                      # explicitly synthetic schedule adjustments
  energy_balance/                 # PV/demand/share conservation
  impact_metrics/                 # sourced cost/carbon/benefit screening
  models/                         # every trained artifact and model manifest
datasets/
  raw/                            # original data, cadastral geometry, IWEC weather
  processed/                      # derived training tables and future case series
  inputs/                         # empty case-study templates; no invented host
  synthetic/energyplus/            # per-scenario physical inputs, outputs and logs
  results/                        # benchmark metrics and held-out predictions
reports/
  data_audit/                     # source/column quality and preparation evidence
  demand_model/                   # measured-data results; initial experiment archive
  simulation_surrogate/           # physics setup, splits, evidence and model card
  verification/                   # clearly labeled synthetic inference checks
docs/                             # methods and input/output contracts
tests/                            # focused correctness checks
tools/energyplus/                  # portable official engine and reference examples
```

No trained model is stored inside `datasets/`. Large local inputs, derived training
tables, simulator output directories and model binaries are ignored by Git;
configuration, source code and compact evidence remain reviewable. No Git commit
or deployment is performed by this setup.
