# Dynamic Physician Scheduling in Emergency Department: Experimental Data & Results  
This repository contains experimental data and solution results supporting the paper **"Dynamic Physician Scheduling in Emergency Departments among Different Rooms with Uncertain Patient Arrivals"** 
## Repository Structure  
The repository is organized into two main directories: `data` (experimental input data) and `solution_results` (detailed results), corresponding to the numerical experiments in the paper.  


### 1. Data Directory (`data/`)  
This directory contains input parameters and raw data for all numerical experiments, categorized into subdirectories aligned with the paper’s experiment sections (Section 6: Numerical Experiments):  

- **`small_scale_instance/`**  
  Contains 10 text files named `case_<number>.txt` (e.g., `case_1.txt`), corresponding to the small-scale test instances in **Section 6.2 (Small-Scale Instance Experiments)**. Each file includes parameters such as: the number of periods (\( T \)), physician counts in each period (\( N_t \)), patient arrival rates in each period (\( lam0, lam1 \)), service rates (\( mu_0, mu_1 \)), cost coefficients (\( c_0, c_1, p_0, p_1 \)), capacity limits (\( \bar{q}_0, \bar{q}_1 \)), initial patient counts in the system (\( q0_initial, q1_initial \)), and maximum patient count limits (\( q0_max, q1_max \)).  

- **`non-epidemic_phase/`**  
  Contains 10 text files named `case_<date>.txt` (e.g., `case_2022-08-10.txt`), corresponding to real ED data from the non-epidemic period in **Section 6.3 (Non-epidemic Phase Experiment)**. These files include the same parameters as those in the `small_scale_instance/` directory, plus additional data such as: forecast patient arrival rates via moving average (\( history_lam0, history_lam1 \)), forecast patient arrival rates via MLR-OL (\( forecast_lam0, forecast_lam1 \)), and physician shift schedules.  

- **`epidemic_phase/`**  
  Contains 10 text files named `case_<date>.txt` (e.g., `case_2022-12-25.txt`), corresponding to real ED data from the epidemic period in **Section 6.4 (Epidemic Phase Experiment)**. These files include the same parameters as those in the `non-epidemic_phase/` directory.  

- **`sensitivity_analysis_instances/`**  
  Contains 105 text files for **Section 6.5 (Sensitivity Analysis)**, including:  
  - 5 baseline files (`case_<date>.txt`) with unmodified parameters.  
  - 25 files with 5 different values for the LOS cost coefficient \( c_0 \) (`case_<date>c0_<value>.txt`).  
  - 25 files with 5 different values for the penalty cost coefficient \( p_0 \) (`case_<date>p0_<value>.txt`).  
  - 25 files with 5 different values for the critical patient capacity limit \( \bar{q}_0 \) (`case_<date>q0_hat_<value>.txt`).  
  - 25 files with 5 different values for the mild patient capacity limit \( \bar{q}_1 \) (`case_<date>q1_hat_<value>.txt`).  


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
