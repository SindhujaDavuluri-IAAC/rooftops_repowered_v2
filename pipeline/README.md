# Model pipeline

Separate work folders for the demand models specified in `../PIPELINE.md`:

- `demand_xgboost/`: primary trained hourly electricity-demand model.
- `demand_baseline_hour_of_week/`: building-type and hour-of-week reference baseline.
- `demand_baseline_seasonal/`: seasonal reference baseline.
- `models/`: saved trained models and their feature schemas/training manifests.

Additional components:

- `data_audit/`: streaming source quality reports.
- `demand_preparation/`: BDG2 joins, features and disjoint building partitions.
- `simulation_surrogate/`: EnergyPlus office scenarios, training and restricted inference.
- `pvgis/`: explicit PVGIS power-to-hourly-energy import.
- `scenarios/`: manually supplied schedule adjustments, clearly labeled synthetic.
- `energy_balance/`: four allocation comparisons with strict conservation.
- `impact_metrics/`: sourced cost/emissions and gross participant-benefit screening.

Run `python -m pipeline --help` from the project root. Models are implemented;
see generated model cards under `reports/` for the actual benchmark outcomes.
BDG2 XGBoost did not beat the primary baseline. The office simulator-surrogate is
the agreed next AI route; measured BDG2 experiments remain as benchmarks.

Save every trained artifact under `pipeline/models/` relative to the project root.
Keep original/processed data under `datasets/`. The host is configured separately
in `config/project.json` and remains unset.

PV generation uses PVGIS exports. Allocation and impacts are deterministic accounting,
not extra AI models. EnergyPlus supplies synthetic physical training targets for
the alternative demand surrogate; no new solar physics model is trained.
