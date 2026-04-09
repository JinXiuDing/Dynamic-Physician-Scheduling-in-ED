# Dynamic Physician Scheduling in Emergency Department: Experimental Data & Results  
This repository contains experimental data and solution results supporting the paper **"Dynamic Physician Scheduling in Emergency Departments among Different Rooms with Uncertain Patient Arrivals"** 
## Repository Structure  
The repository is organized into two main directories: `data` (experimental input data) and `solution_results` (detailed results), corresponding to the numerical experiments in the paper. 

## 1. Data Directory (`data/`)
This directory contains all input parameters and raw experimental data in standardized Excel (.xlsx) format. Each Excel file corresponds to one experiment type in Section 6, with one worksheet per test case; the sheet name is the case name (e.g., `case_2022-12-25`).

All files follow a unified table format:
- Each row represents one parameter field. The definition of each field is listed in the table below.
- Columns `v1–v24` represent values for 24 consecutive periods (1 hour per period).
- Time-invariant parameters (e.g., service rates) that remain fixed for the entire decision horizon are entered only in column `v1`.

### Unified Data Field Definitions
| Field             | Meaning                                                                 |
|--------------------|-------------------------------------------------------------------------|
| T                  | Total number of periods    |
| lam0               | Actual arrival rate of critical patients per period                      |
| lam1               | Actual arrival rate of mild patients per period                          |
| forecast_lam0      | MLR-OL method predicted arrival rate of critical patients per period             |
| forecast_lam1      | MLR-OL method predicted arrival rate of mild patients per period                 |
| history_lam0       | Moving average (MA) method predicted arrival rate of critical patients per period |
| history_lam1       | Moving average (MA) method predicted arrival rate of mild patients per period     |
| mu0                | Physician service rate in resuscitation room    |
| mu1                | Physician service rate in general consultation rooms              |
| c0                 | Unit time LOS cost for each critical patient                                 |
| c1                 | Unit time LOS cost for each mild patient                                   |
| p0                 | Additional unit time penalty when the number of critical patients exceeds capacity limit|
| p1                 | Additional unit time penalty when the number of mild patients exceeds capacity limit   |
| q0_hat             | Capacity limit for the number of critical patients in the system                      |
| q1_hat             | Capacity limit for the number of mild patients in the system                       |
| q0_initial         | Initial number of critical patients in the system                       |
| q1_initial         | Initial number of mild patients in the system                           |
| q0_max             | State space upper bound for critical patients       |
| q1_max             | State space upper bound for mild patients            |
| N_t                | Number of available physicians in each period                             |

### Excel File Details
- **`small_scale_instances.xlsx`**
10 test cases for **Section 6.2 (Small-Scale Instance Experiments)**. 

- **`non-epidemic_phase.xlsx`**
  10 real ED cases for **Section 6.3 (Non-epidemic Phase Experiment)**. 

- **`epidemic_phase.xlsx`**
  10 real ED cases for **Section 6.4 (Epidemic Phase Experiment)**. 

- **`sensitivity_analysis_instances.xlsx`**
  105 cases for **Section 6.5 (Sensitivity Analysis)**, including: 
  - 5 baseline cases (unchanged parameters)
  - 25 cases with varied critical patient waiting cost *c₀*
  - 25 cases with varied critical patient penalty cost *p₀*
  - 25 cases with varied critical patient capacity limit *q̅₀*
  - 25 cases with varied mild patient capacity limit *q̅₁*

### 2. Solution Results Directory (`solution_results/`)  
This directory contains detailed experimental results in Excel files, matching the structure of the `data` directory:  

- **`small_scale_instances.xlsx`**  
  Results for **Section 6.2**. For each small-scale instance:  
  - A bold row shows the total expected cost across the decision horizon for the following methods: BI-PI, BI, Gcμ, CP, and MP.  
  - Per-period rows include the expected cost for each method and the average number of critical (`avg_q0`) and mild (`avg_q1`) patients at the end of each period.  

- **`non-epidemic_phase.xlsx`**  
  Results for **Section 6.3**. For each non-epidemic phase instance:  
  - A bold row shows the total expected cost for the following methods: BI1, $\overline{\text{BI1}}$ $\widehat{BI1}$, $\widehat{BI2}$,Gcμ, CP, MP, and FA.  
  - 24 rows include per-period costs and patient counts (`avg_q0`, `avg_q1`).  

- **`epidemic_phase.xlsx`**  
  Results for **Section 6.4**. Structured identically to `non-epidemic_phase.xlsx`, with results for the same methods during the epidemic phase.  

- **`sensitivity_analysis.xlsx`**  
  Results for **Section 6.5**. Columns include:  
  - `Date`: Base date of the instance.  
  - `Parameter Setting`: Modified parameter values (e.g., \( c_0=2 \)) or "baseline instance" for unmodified parameters.  
  - `BI1` and `Gcμ`: Expected costs for the proposed method and the benchmark gcμ rule.  
  - Bold rows show average results across five instances for each parameter setting.
