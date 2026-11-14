# Project progress and next steps

## Completed foundation

- Downloaded and structurally audited all eight core datasets plus Barcelona
  cadastral geometry. Full field-level missingness and meter ranges are in
  `reports/data_audit/column_quality.csv`.
- The Barcelona 2025 consumption export covers January–November only. Certificates
  are modeled energy-performance records, not measured consumption.
- Prepared a 70-building pilot and a 310-building expanded BDG2 cohort. The expanded
  table has 5,258,034 retained measured hourly readings.
- Trained two baselines and XGBoost, with disjoint buildings and reproducible inputs.
  Both measured-data XGBoost experiments failed the primary MAE gate. No local
  Barcelona accuracy is claimed. The initial experiment is archived separately.
- Implemented PVGIS import, UTC alignment, explicit schedule adjustment, share-plan
  generation, four energy scenarios and sourced impact-screening code.
- Added host-free configuration and empty case-study templates. Every trained model
  belongs under `pipeline/models/`.

## Office physics route

The user selected this route after the measured-data experiment, starting with
office archetypes only. Portable EnergyPlus and Barcelona IWEC reference weather
are available locally. An annual office smoke simulation succeeded. The full grid
contains 36 completed operating configurations (315,360 simulated hourly targets).
The surrogate passed both validation and test comparisons against the hourly and
schedule-aware linear baselines. Test MAE is 0.648 kWh/hour versus 1.465 for the
linear baseline and 2.335 for the hourly baseline. Test NMAE is 11.96% of mean
simulated demand. The partitions contain 22 training, 7 validation and 7 test
configurations; none shares a configuration with another partition.

The model and its manifest are saved in `pipeline/models/`. Both
`reports/simulation_surrogate/MODEL_CARD.md` and `readiness.json` record the outcome.
The generic `predict` command now uses this configured office-surrogate route;
`predict-bdg2` retains the measured-data benchmark. Saved-model CLI inference was
checked on 168 synthetic reference hours against direct model predictions.

Simulation validation excludes entire operation configurations. Its geometry,
HVAC and envelope are one published U.S. office reference, with Barcelona weather
and design days. Results describe simulator approximation, not measured local
building behavior. New geometry and other uses require domain expansion.

## Deferred until the real case study is selected

1. Host roof and 3–5 participant buildings, building functions, floor areas and sources.
2. Usable rooftop capacity, tilt/azimuth/losses and selected-roof PVGIS export.
3. Explicit representative-year/calendar convention and sourced hourly weather;
   inspect PVGIS minute offsets before joining to demand.
4. Evidence-backed archetype/operation parameters for the selected buildings. The
   office surrogate cannot silently scale one reference geometry to arbitrary areas.
5. Independently held-out demand references for testing allocation value; do not
   score a forecast-derived plan against that same forecast and call it validation.
6. Dated tariffs, PV capex/O&M, emissions year/boundary and cost/benefit-sharing choices.
7. Legal eligibility/settlement verification before making compliance claims.

The next practical step is to review the office surrogate's model card, then decide
which geometry/operation ranges to expand before applying it to actual buildings.
Interface work follows those results; no citywide or live-control functionality is planned.
