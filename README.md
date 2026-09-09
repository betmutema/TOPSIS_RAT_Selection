# TOPSIS-Based Radio Access Technology Selection in Heterogeneous Networks

## Overview

This project implements a multi-criteria decision-making framework for selecting the optimal Radio Access Technology (RAT), 3G, 4G LTE, or Wi-Fi, in a heterogeneous wireless environment. Rather than optimizing for a single factor, the framework evaluates bandwidth, cost, and delay simultaneously using TOPSIS (Technique for Order of Preference by Similarity to Ideal Solution), producing a RAT ranking that adapts to the priorities of the individual user rather than defaulting to a fixed, rule-based selection.

## Why TOPSIS

Three multi-criteria methods were considered:

- **AHP (Analytic Hierarchy Process)**: primarily useful for deriving criterion weights, not for directly ranking alternatives.
- **SAW (Simple Additive Weighting)**: computes a weighted sum, which is too simplistic when the best option isn't necessarily the one that maximizes a single weighted score.
- **TOPSIS**: ranks each RAT by its distance from both an ideal solution and a negative-ideal (worst-case) solution, making it well suited to a trade-off ranking problem where no single network dominates on every criterion.

## Methodology

The complete TOPSIS pipeline implemented here:

1. Construct the decision matrix for 3G, 4G LTE, and Wi-Fi across three criteria: bandwidth, cost, and delay.
2. Normalize the criteria and apply user-defined weights.
3. Compute the ideal and negative-ideal solutions, correctly distinguishing benefit criteria (bandwidth, maximized) from cost criteria (cost and delay, minimized).
4. Rank the RATs by their closeness coefficients.

## Simulation Setup

The framework is evaluated using a MATLAB simulation with 100 simulated users, each assigned randomly generated criterion weights within a defined scale. Bandwidth, cost, and delay values per network are representative scenario parameters rather than live network measurements, the goal is to evaluate the selection methodology itself, not to benchmark a specific operator's real-world performance.

Randomly generated weights map onto realistic user behavior:
- High bandwidth weight → a user prioritizing high-throughput applications (e.g., streaming)
- High cost weight → a budget-conscious user
- High delay weight → a user prioritizing low latency (e.g., gaming, real-time communication)

## Key Findings

- **Bandwidth had by far the largest influence** on final RAT selection.
- Under balanced/random weighting, average closeness coefficients were: **4G LTE ≈ 0.725**, **Wi-Fi ≈ 0.403**, **3G ≈ 0.115**.
- When bandwidth was assigned maximum importance, selection became decisive: every simulated user chose 4G LTE. Reducing bandwidth's importance shifted the dominant choice to 3G.
- Changing cost and delay weighting produced corresponding shifts, e.g., increasing cost weighting made users more willing to trade performance for lower operating cost.
- **No RAT is universally optimal.** Selection outcome is highly sensitive to the relative priorities assigned to bandwidth, cost, and delay, supporting a multi-criteria approach over a fixed, rule-based mechanism.
- An unexpected result: increasing one criterion's weight to an extreme didn't shift preference gradually, it produced unanimous selection of the same RAT across all 100 simulated users.

## Limitations and Future Work

- Network parameters (bandwidth, cost, delay) are fixed, assumed values rather than live network measurements.
- Simulated "users" are randomly generated weight sets, not explicitly modeled user personas.

A more realistic implementation would incorporate:
- Live measurements of bandwidth, latency, and network cost
- Explicitly defined user profiles representing different application requirements
- Time-varying network conditions and changing user mobility
- Real-time or periodically updated RAT selection

## Repository Structure

```
├── EEE4121F_Project_MTMBRE002_2024.pdf   # Full project report
├── EEE4121F_Project_MTMBRE002_Code.mlx   # MATLAB Live Script: full TOPSIS implementation and simulation
└── README.md
```

## Requirements

- MATLAB (developed and tested in [version, if known])
- No additional toolboxes required beyond base MATLAB *(update if you used any, e.g. Statistics and Machine Learning Toolbox)*

## Usage

Open `EEE4121F_Project_MTMBRE002_Code.mlx` in MATLAB and run it as a Live Script. The full pipeline, decision matrix construction, normalization, weighting, ideal/negative-ideal solution calculation, and the 100-user simulation, runs top to bottom in one file, with results and plots generated inline.

## About

Individual project: full ownership of algorithm selection, implementation, and evaluation, part of EEE4121F.
