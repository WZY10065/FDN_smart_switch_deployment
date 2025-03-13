# High-Reliability Flexible Distribution Network Switch Configuration Optimization

This repository contains the optimization results and detailed analysis for the switch configuration in a high-reliability flexible distribution network (FDN), as presented in Chapter 4 of the study titled *"High-Reliability Flexible Distribution Network Switch Optimal Configuration Method"*. The study focuses on the synergistic deployment of multiple types of intelligent switches—namely **Circuit Breakers (CB)**, **Remote-Controlled Switches (RCS)**, and **Soft Open Points (SOP)**—to enhance the reliability and self-healing capability of flexible distribution networks under various fault scenarios.

## Project Overview

In modern urban flexible distribution networks, the optimal configuration of intelligent switches is critical for improving fault isolation, self-healing, and overall system reliability. This project proposes a novel optimization model that integrates explicit reliability expressions to jointly configure **CB**, **RCS**, and **SOP** devices. The model accounts for the dynamic topological changes during fault self-healing processes and leverages the unique capabilities of SOPs for power restoration and voltage support.

### Key Contributions
1. **Explicit Reliability Modeling with SOP**: We developed an explicit reliability model that captures the interaction between SOP, CB, and RCS during fault self-healing, enabling efficient optimization of switch configurations.
2. **High-Reliability Planning Model**: A planning decision model was formulated to achieve optimal reliability and economic performance, surpassing traditional planning-evaluation methods and heuristic optimization approaches.
3. **Adaptive Progressive Hedging (APH) Algorithm**: We proposed an APH algorithm to solve the two-stage stochastic mixed-integer programming model, addressing the challenges of topological variations and multi-variable coupling in large-scale scenarios.

### Case Study
The proposed model was tested on a 40-node network with four interconnected feeders, as detailed in the study. The system operates at 10 kV, and the specific topology is provided in Appendix B of the original document. Three configuration strategies were compared:
- **Strategy I**: Joint configuration of CB, RCS, and SOP.
- **Strategy II**: CB at feeder exits only, with RCS elsewhere.
- **Strategy III**: Flexible CB and RCS configuration without SOP.

## Optimization Results
![CaseI_Fault_Scenario_13](https://github.com/user-attachments/assets/2853d162-4cef-485e-a991-75c5c2db3c3b)

To demonstrate the performance of the proposed switch configuration strategies, we analyzed the fault scenario where a fault occurs on the line between nodes 10 and 11. The results for each strategy across different stages of the fault self-healing process—**Normal Operation (NO)**, **Fault Degradation (FD)**, **Fault Isolation (FI)**, and **Service Restoration (SR)**—are illustrated in the figures below.

### Visualization of Results

The following figures showcase the topological changes and switch actions for a fault on line (10, 11) under **Strategy I** (CB, RCS, and SOP joint configuration). The nodes and lines are color-coded as follows:
- **Red (CB)**: Circuit Breaker
- **Yellow (RCS)**: Remote-Controlled Switch
- **Green (SOP)**: Soft Open Point
- **Blue Nodes**: Load nodes with power supply
- **Red Nodes**: Load nodes without power (fault-affected)
- **Gray Area**: Fault-affected region


### Full Results
The figures above represent a subset of the results for **Strategy I** under fault scenario 0 (line 10-11). The complete set of results, including topological changes for all strategies (I, II, and III) across 39 fault scenarios, 4 stages, and 3 strategies (totaling 468 figures), is available in the `figures/` directory of this repository.

#### Directory Structure
- `figures/`: Contains all topological diagrams for each strategy, stage, and fault scenario.
  - Example: `strategy_I_NO_scenario_0.png` represents Strategy I, Normal Operation stage, scenario 0.
- `data/`: Contains raw data files, such as switch configuration variables and reliability metrics for each scenario (if applicable).
- `code/`: Includes the Python scripts used for optimization and visualization (if shared).

## Performance Comparison

The performance of the three strategies was evaluated based on reliability metrics, switch deployment, and economic costs. The results are summarized in the table below:

| **Strategy** | **SAIDI (h/year)** | **SAIFI (1/year)** | **EENS (MWh/year)** | **ASAI (%)** | **N_{CB}** | **N_{RCS}** | **N_{SOP}** | **C_{rel} (万元)** | **C_{inv} (万元)** | **C (万元)** |
|--------------|--------------------|--------------------|---------------------|--------------|---------|----------|----------|----------------|----------------|-------------|
| **Strategy I** | 0.4044            | 0.7777            | 1.3504             | 99.9954      | 16      | 39       | 2        | 67.52         | 38.28         | 105.80      |
| **Strategy II** | 1.1402           | 2.8574            | 4.1957             | 99.9870      | 4       | 55       | 0        | 209.78        | 16.45         | 226.23      |
| **Strategy III** | 0.7173          | 1.1656            | 2.5237             | 99.9918      | 16      | 43       | 0        | 126.19        | 23.19         | 149.38      |

### Key Observations
- **Strategy I** (with SOP) outperforms the other strategies in all reliability metrics (SAIDI, SAIFI, EENS, and ASAI), highlighting SOP's advantages in fault isolation, load transfer, and voltage support.
- While Strategy I has a higher investment cost (Cinv) due to SOP deployment, it significantly reduces reliability-related costs (Crel), making it the most cost-effective option overall (lowest total cost, C).
- **Strategy III** performs better than Strategy II by allowing flexible CB placement, which reduces the fault-affected area during the FD stage compared to Strategy II's feeder-exit-only CB configuration.

## How to Use This Repository

1. **Explore the Figures**:
   - Navigate to the `figures/` directory to view the topological changes for each strategy, stage, and fault scenario.
   - Figures are named in the format `strategy_[I/II/III]_[stage]_scenario_[number].png`.

2. **Analyze the Data**:
   - The `data/` directory (if provided) contains detailed switch configuration variables, load states, and reliability metrics for each scenario.

3. **Run the Code** (if applicable):
   - The `code/` directory includes Python scripts for optimization and visualization.
   - Requirements: Python 3.11, Gurobi 12.0, and necessary dependencies (e.g., NumPy, Matplotlib).
   - Example command to run the visualization script:
     ```bash
     python code/visualize_topology.py --strategy I --scenario 0
