# Multi-Product Demand Allocation MILP

A synthetic mixed-integer linear programming project for allocating multiple product demands across production facilities while minimizing production, transportation, and capacity-expansion costs.

The project is intentionally generic. It does not use proprietary data, company names, or real operational datasets.

## Problem Overview

The model decides:

- how many units of each product should be produced at each facility,
- how those units should be allocated to demand markets,
- whether additional production capacity should be activated,
- how much additional capacity should be added.

The objective is to minimize the total annualized cost while satisfying demand, capacity, routing, production-availability, and minimum-utilization requirements.

## Optimization Model

The implementation uses `scipy.optimize.milp` with HiGHS.

Decision variables:

- `x[i,j,p]`: integer units of product `p` produced at facility `i` and shipped to market `j`
- `y[i,p]`: binary capacity-expansion activation variable
- `a[i,p]`: integer added capacity for product `p` at facility `i`

The objective includes:

- unit production cost,
- unit transportation cost,
- fixed capacity-expansion cost,
- variable capacity-expansion cost,
- capital-recovery annualization of capacity-expansion expenditures.

Main constraints:

1. Demand satisfaction for every market-product pair.
2. Product-specific production-capacity limits.
3. Route and production-availability restrictions.
4. Facility-level minimum utilization requirements.
5. Capacity-expansion activation and upper-bound constraints.
6. Integrality and binary restrictions.

## Repository Structure

```text
.
├── README.md
├── LICENSE.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── facilities.csv
│   ├── products.csv
│   ├── markets.csv
│   ├── demand.csv
│   ├── production_capacity.csv
│   ├── production_cost.csv
│   ├── transportation_cost.csv
│   ├── route_availability.csv
│   ├── production_availability.csv
│   └── capacity_expansion.csv
├── docs/
│   └── mathematical_model.md
└── src/
    ├── generate_data.py
    ├── model.py
    ├── solve.py
    └── reporting.py
```

## Installation

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## Generate Synthetic Data

```bash
python src/generate_data.py
```

The generator creates a reproducible synthetic instance under `data/`.

## Solve the Optimization Model

```bash
python src/solve.py
```

The solver writes result files to `outputs/` and prints a compact summary to the terminal.

## Notes

This repository is designed for educational, academic, research, and portfolio use. It is not intended to represent any specific company, commercial system, or proprietary planning process.

## License

This project is released under a custom non-commercial license. Commercial use is not permitted without prior written permission. See `LICENSE.md` for details.
