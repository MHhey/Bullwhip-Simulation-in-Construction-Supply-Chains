# Agentic AI Simulation of Bullwhip Effect in Construction Supply Chains

> Heydari, M., Shojaei, A., McCoy, A., & Akanmu, A. — Myers-Lawson School of Construction, Virginia Tech

## About

The bullwhip effect is a well-known supply chain phenomenon where small demand fluctuations at the project site amplify dramatically as they propagate upstream through the chain. This repository contains an **agentic AI simulation framework** to study how this amplification manifests in construction supply chains under different network topologies and information-sharing regimes.

Unlike traditional agent-based models that rely on fixed decision rules, each supply chain agent here calls an **LLM (Gemini)** at every time step to generate adaptive behavioral coefficients — responsiveness, service level, order sizing, and expediting decisions — based on its role, current inventory state, and visible demand signals. This enables emergent behaviors such as defensive stockpiling to arise naturally from the simulation rather than being hardcoded.

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

> Notebook numbering follows topology grouping; scenario numbers in comments match the paper.

## Supply Chain Structure

**Linear (forward chain):**
```
Supplier → Distributor → 3PL → Procurement Office → Contractor
```
**Circular (closed-loop), adds a reverse flow:**
```
Contractor → Collection Point → Material Recovery → Supplier
```
Steel waste is recovered at 90% and re-enters the supplier's inventory after a 6-week reverse lead time.

## Agent Decision Making

At each weekly time step, every agent calls the LLM to generate a behavioral coefficient vector:

| Coefficient | Range | Meaning |
|---|---|---|
| `alpha` | [0.05, 0.50] | Responsiveness to recent demand signals |
| `service_level` | [0.80, 0.95] | Target stockout avoidance probability |
| `lot_multiplier` | [0.50, 2.00] | Order size relative to base-stock gap |
| `expedite` | true / false | Pay a premium to accelerate delivery |

Outputs are schema-constrained JSON validated before entering the inventory math. Demand data is drawn from the EU Horizon 2020 construction project dataset (steel, 52-week horizon, disruption at week 30).

## How to Use

**Reproduce the paper results:** Run any notebook as-is from top to bottom.

**Adapt to your own research:**
- Swap in your own demand data in the `customerDemand` array (R1 cell)
- Change `info_regime` between `"local"`, `"global"` to compare information sharing effects
- Edit `ROLE_STRATEGIES` prompts to model different agent behaviors or supply chain contexts
- Extend `ROLES` and `FLOW` to test different network configurations

## Requirements

```bash
pip install google-generativeai jsonschema numpy pandas scipy matplotlib seaborn
```

Set your Gemini API key before running:
```bash
export GEMINI_API_KEY="your_key_here"
```

## License

MIT
