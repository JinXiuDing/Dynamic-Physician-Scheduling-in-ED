# Dynamic Physician Scheduling in Emergency Department: Data and Results
This repository contains input data and computational results for the paper:
**"Dynamic Physician Scheduling in Emergency Departments among Different Rooms with Uncertain Patient Arrivals"**.

## Repository Structure
The repository is organized into two main directories: `data` (experimental input data) and `solution_results` (detailed results), corresponding to the numerical experiments in the paper (Section 6).

---

## 1. Data Directory (`data/`)
This directory stores **all input parameters and raw experimental data in standardized Excel (.xlsx) format** (revised from plain text for readability and interpretability). Each Excel file corresponds to one experiment type in Section 6, with **one worksheet (sheet) per test case**; the sheet name is the case identifier (e.g., `case_2022-12-25`).

All files use a **unified field-variable format** with clear column definitions:
- Rows: parameter fields (consistent with paper notation)
- Columns `v1–v24`: hourly values for 24 periods (1 hour per period)
- Scalar parameters (fixed for the full decision horizon) fill only column `v1`

### Unified Data Field Definitions
| Field             | Meaning                                                                 |
|--------------------|-------------------------------------------------------------------------|
| T                  | Total number of periods (fixed to 24 hours for all cases)               |
| lam0               | Actual arrival rate of critical patients per hour                      |
| lam1               | Actual arrival rate of mild patients per hour                          |
| forecast_lam0      | MLR-OL predicted arrival rate of critical patients per hour             |
| forecast_lam1      | MLR-OL predicted arrival rate of mild patients per hour                 |
| history_lam0       | Moving average (MA) predicted arrival rate of critical patients per hour |
| history_lam1       | Moving average (MA) predicted arrival rate of mild patients per hour     |
| mu0                | Physician service rate in resuscitation room (patients per hour, PPH)   |
| mu1                | Physician service rate in general consultation rooms (PPH)              |
| c0                 | Unit waiting cost for critical patients                                 |
| c1                 | Unit waiting cost for mild patients                                     |
| p0                 | Overflow penalty cost coefficient for critical patients                 |
| p1                 | Overflow penalty cost coefficient for mild patients                     |
| q0_hat             | Capacity limit (threshold) for critical patients                       |
| q1_hat             | Capacity limit (threshold) for mild patients                           |
| q0_initial         | Initial number of critical patients in the system                       |
| q1_initial         | Initial number of mild patients in the system                           |
| q0_max             | Maximum possible number of critical patients (state space bound)       |
| q1_max             | Maximum possible number of mild patients (state space bound)            |
| N_t                | Number of available physicians in each hour                             |

### Excel File Details
- **`small_scale_instances.xlsx`**
  10 test cases for **Section 6.2 (Small-Scale Instance Experiments)**. Includes core scheduling parameters: T, N_t, lam0, lam1, mu0, mu1, cost coefficients, capacity bounds, initial states, max patient limits.

- **`non-epidemic_phase.xlsx`**
  10 real ED cases for **Section 6.3 (Non-epidemic Phase Experiment)**. Includes all small-scale parameters plus MA and MLR-OL arrival forecasts.

- **`epidemic_phase.xlsx`**
  10 real ED cases for **Section 6.4 (Epidemic Phase Experiment)**. Same fields as non-epidemic phase, covering high-fluctuation pandemic-period data.

- **`sensitivity_analysis_instances.xlsx`**
  105 cases for **Section 6.5 (Sensitivity Analysis)**:
  - 5 baseline cases (unchanged parameters)
  - 25 cases with varied critical patient waiting cost *c₀*
  - 25 cases with varied critical patient penalty cost *p₀*
  - 25 cases with varied critical patient capacity limit *q̅₀*
  - 25 cases with varied mild patient capacity limit *q̅₁*

---

## 2. Solution Results Directory (`solution_results/`)
This directory contains detailed experimental results in Excel files, with structure matching the `data` directory for direct traceability.

- **`small_scale_instances.xlsx`**
  Results for **Section 6.2**:
  - Bold row: total expected cost for BI-PI, BI, Gcμ, CP, MP
  - 24 hourly rows: per-period cost + average critical (`avg_q0`) / mild (`avg_q1`) patient counts

- **`non-epidemic_phase.xlsx`**
  Results for **Section 6.3**:
  - Bold row: total cost for BI1, $\overline{\text{BI1}}$, $\widehat{\text{BI1}}$, $\widehat{\text{BI2}}$, Gcμ, CP, MP, FA
  - 24 hourly rows: per-period cost and average patient counts

- **`epidemic_phase.xlsx`**
  Results for **Section 6.4**: same structure as non-epidemic phase, for pandemic-period cases.

- **`sensitivity_analysis.xlsx`**
  Results for **Section 6.5**:
  - Columns: Date (case date), Parameter Setting (modified parameter + value), BI1 (cost), Gcμ (benchmark cost)
  - Bold rows: average performance across 5 instances per parameter setting

---

## Notes
- All time-dependent parameters use **24 hourly values** (one hour per period) consistent with ED operational scheduling.
- Field notation strictly follows the mathematical definitions in the paper for full reproducibility.
