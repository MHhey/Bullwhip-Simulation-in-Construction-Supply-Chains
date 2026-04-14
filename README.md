# Agentic AI Simulation of Bullwhip Effect in Construction Supply Chains

## About

This repository contains simulation code for studying how the **bullwhip effect** propagates through construction supply chains under different network topologies and information-sharing regimes. Instead of fixed decision rules, each supply chain agent calls an **LLM (Gemini)** at every time step to generate adaptive behavioral coefficients, enabling emergent behaviors like defensive stockpiling to arise naturally.

## Scenarios

12 self-contained Jupyter notebooks covering a full factorial design:

| Dimension | Levels |
|---|---|
| Network topology | Linear · Circular (closed-loop with material recovery) |
| Project scope | Single-project · Multi-project |
| Information regime | Local · Global · Efficient |

## Repository Structure

```
├── 1_Linear_Single_Local_5ech.ipynb      # Scenario 1  — Linear, Single, Local
├── 2_Linear_Single_Global_5ech.ipynb     # Scenario 2  — Linear, Single, Global
├── 3_Linear_Multi_Local_5ech.ipynb       # Scenario 4  — Linear, Multi,  Local
├── 4_Linear_Multi_Global_5ech.ipynb      # Scenario 5  — Linear, Multi,  Global
├── 5_Circular_Single_Local_5ech.ipynb    # Scenario 7  — Circular, Single, Local
├── 6_Circular_Single_Global_5ech.ipynb   # Scenario 8  — Circular, Single, Global
├── 7_Circular_Multi_Local_5ech.ipynb     # Scenario 10 — Circular, Multi,  Local
├── 8_Circular_Multi_Global_5ech.ipynb    # Scenario 11 — Circular, Multi,  Global
├── 9_Linear_Single_Eff_5ech.ipynb        # Scenario 3  — Linear, Single, Efficient
├── 10_Linear_Multi_Eff_5ech.ipynb        # Scenario 6  — Linear, Multi,  Efficient
├── 11_Circular_Single_Eff_5ech.ipynb     # Scenario 9  — Circular, Single, Efficient
└── 12_Circular_Multi_Eff_5ech.ipynb      # Scenario 12 — Circular, Multi,  Efficient
```

## Requirements

```bash
pip install google-generativeai jsonschema numpy pandas scipy matplotlib seaborn
```

Set your Gemini API key before running:
```bash
export GEMINI_API_KEY="your_key_here"
```

Each notebook is self-contained — run cells sequentially from top to bottom.
