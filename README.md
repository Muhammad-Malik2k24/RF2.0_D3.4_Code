```markdown
# Research Facility 2.0 Energy Systems

Energy management, forecasting, and climate scenario tools for renewable energy systems with battery storage.  
**License:** [EUPL v1.2 or later](https://joinup.ec.europa.eu/collection/eupl/eupl-text-eupl-12)  
**Copyright:** © 2025 Research Facility 2.0 Consortium

---

## Table of Contents

- [Overview](#overview)
- [License](#license)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Input Data Format](#input-data-format)
- [Configuration](#configuration)
- [Output Files](#output-files)
- [Optional Components](#optional-components)
- [Troubleshooting](#troubleshooting)
- [Citation](#citation)
- [Support](#support)
- [Contributing](#contributing)
- [Acknowledgments](#acknowledgments)
- [Core Dependencies](#core-dependencies)
- [License Summary](#license-summary)

---

## Overview

This repository provides tools for:
- **PV Generation Forecasting:** AutoML neural network models for solar power prediction.
- **Battery MPC Optimization:** Model predictive control for advanced battery energy storage systems.
- **Climate Scenario Analysis:** Probabilistic PV generation scenarios based on global SSP climate pathways.

These tools are designed for academics, researchers, and engineers working on optimal design and operation of renewable-based hybrid energy systems.

---

## License

This code is distributed under the European Union Public Licence (EUPL) v1.2 or later.  
You are free to use, modify, and distribute it under the terms outlined in the license.  
See the [LICENSE](LICENSE) file for full details.

---

## Installation

**Requirements:**
- Python 3.9 or higher
- Minimum 8 GB RAM (16 GB recommended)
- Works on Windows, Linux, macOS

**Install all dependencies:**

```
pip install -r requirements.txt
```

*All required libraries are open-source. Optional commercial or GPU features are available; see below.*

**Verify installation:**

```
import numpy, pandas, cvxpy, torch, pvlib
print("✓ All packages installed successfully!")
```

---

## Quick Start

Examples:

**1. PV Forecasting**

```
python pv_forecasting.py
```

Requires a CSV file with `PV_generation_kW` column (15-min resolution).

**2. Battery MPC**

```
python mpc_battery_optimization.py
```

Requires a CSV file with `PV_generation_kW` and `load_demand_kW` columns.

**3. Climate Scenarios**

```
python climate_scenarios.py
```

Requires SSP climate projection files (CORDEX/CMIP6 format).

---

## Input Data Format

**For PV Forecasting & Battery MPC:**
```
timestamp,PV_generation_kW,load_demand_kW
2024-01-01 00:00:00,0.0,450.2
2024-01-01 00:15:00,0.0,442.8
...
```

**For Climate Scenarios:**
- Files must contain columns with surface solar radiation (`rsds`) and near-surface air temperature (`tas`), and "SSP" in the filename.

---

## Configuration

**Site Location Example:**
```
SITE_CONFIG = {
    'latitude': 49.0,
    'longitude': 8.4,
    'altitude': 110,
    'timezone': 'Europe/Berlin',
}
```

**Battery System Example:**
```
battery_params = {
    'capacity_per_battery': 0.932,  # MWh
    'max_power_per_battery': 0.466,  # MW
    'efficiency': 0.972,
    'soc_min': 0.05,
    'soc_max': 0.95,
    'n_units': 2,
}
```

**Tariff Example:**
```
tariff_params = {
    'c_energy': 0.40,  # €/kWh
    'c_peak': 80.0     # €/kW/year
}
```

Modify these sections in your scripts as needed.

---

## Output Files

Scripts will save output as CSVs to the working/output directory with names such as:
- `step1_raw_climate_data.csv`
- `step2_climate_with_poa_irradiance.csv`
- `step3_climate_scenarios_kde_quantile.csv`
- `step4_scenarios_with_pv_power.csv`
- `step5_technology_sensitivity_detailed.csv`
- `step6_annual_summary_statistics.csv`
- ...and more.

---

## Optional Components

**Gurobi Solver Support** (Faster optimization, requires separate license):

```
pip install gurobipy
```

See [Gurobi website](https://www.gurobi.com/downloads/) for details.  
**If not installed, the code defaults to open-source solvers (CLARABEL, OSQP)**.

**GPU Support for Neural Networks**:

```
pip install torch --index-url https://download.pytorch.org/whl/cu118
```

Requires NVIDIA GPU + CUDA toolkit.

---

## Troubleshooting

**Import Errors:**  
Update all packages:
```
pip install --upgrade -r requirements.txt
```

**PyTorch CUDA Not Available:**
```
import torch
print(torch.cuda.is_available())  # Should print True if CUDA is working
```

**Gurobi License Error:**  
To use open-source solver, set `use_gurobi=False` in your code.

**Out-of-memory or performance issues:**  
Reduce scenario count or horizon length:
```
n_synthetic_per_ssp = 50  # Reduce if needed
horizon_length = 48
```

---

## Citation

If you use this code, please cite:
```
Research Facility 2.0 Consortium (2025). 
Energy Management and Forecasting Tools for Renewable Energy Systems.
Horizon Europe Project Research Facility 2.0.
https://rf20.eu/
```

---

## Support

- Project website: [https://rf20.eu/](https://rf20.eu/)
- For bugs and issues: please use GitHub Issues

---

## Contributing

Contributions are welcome. Please:
- Follow code style and documentation conventions
- Ensure compatibility with the EUPL v1.2 license
- Add or update tests and documentation as appropriate

---

## Acknowledgments

Supported by Horizon Europe (Research Facility 2.0).

---

## Core Dependencies

| Package        | Purpose                       |
|----------------|------------------------------|
| numpy          | Numerical computing           |
| pandas         | Data manipulation             |
| scipy          | Scientific computing          |
| cvxpy          | Optimization/MPC              |
| torch          | Deep learning                 |
| neuralforecast | Time series forecasting       |
| optuna         | Hyperparameter optimization  |
| pvlib          | Solar modeling                |
| matplotlib     | Plotting                      |
| pytz           | Time zone utilities           |

---

## License Summary

Distributed under the **European Union Public Licence (EUPL) v1.2 or later**.

- Use, modify, distribute under EUPL or compatible licenses.
- Keep copyright/license notices.
- State changes in modified versions.

See the [LICENSE](LICENSE) file for the full text.
```
This README is written in standards-compliant Markdown and ready for direct use on GitHub, GitLab, or other repositories. All relevant instructions, requirements, licensing, and citation details are clearly included.

[1](https://realpython.com/readme-python-project/)
[2](https://www.makeareadme.com)
[3](https://github.com/othneildrew/Best-README-Template)
[4](https://git.ifas.rwth-aachen.de/templates/ifas-python-template/-/blob/master/README.md)
[5](https://packaging.python.org/guides/making-a-pypi-friendly-readme/)
[6](https://www.pyopensci.org/python-package-guide/tutorials/add-readme.html)
[7](https://www.youtube.com/watch?v=12trn2NKw5I)
[8](https://gitlab.cc-asp.fraunhofer.de/ise621/sample-python-project/-/blob/develop/README.md)
[9](https://www.reddit.com/r/opensource/comments/txl9zq/next_level_readme/)
