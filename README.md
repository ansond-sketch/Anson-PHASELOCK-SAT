# Mobile Phase-Lock SAT (Experimental)

A single-file, mobile-safe experimental SAT solver that implements a phase-lock mechanism for solving random 3-SAT instances. Designed for quick reliability sweeps on mobile Python runners.

## Overview

This project explores phase behavior in 3-SAT problems using a distributed local search approach with shared state. Multiple independent "planets" (solver instances) run in parallel, each performing local search while sharing the globally best-known solution.

## What It Does

- **Random 3-SAT Generation**: Generates random 3-SAT instances at configurable clause-to-variable ratios
- **Multi-Planet Architecture**: Runs multiple independent local search instances that cooperate by sharing a best-known state
- **Phase Transition Analysis**: Explores SAT solver behavior around the phase transition threshold (~4.26 for 3-SAT)
- **CSV Logging**: Optional logging of solver state and statistics to CSV for phase behavior analysis
- **Mobile Optimization**: Single-file design using only Python standard library, works on mobile Python runners

## Key Features

- Pure Python 3.10+ implementation
- No external dependencies
- Mobile-safe (uses temp directories for logs)
- Configurable ladder sweeps for systematic phase exploration
- CSV trace output for plotting and analysis
- Thread-safe shared state management

## Requirements

- Python 3.10 or higher
- Works on desktop, cloud, and mobile Python environments

## Installation

Clone the repository:
```bash
git clone https://github.com/ansond-sketch/Anson-PHASELOCK-SAT.git
cd Anson-PHASELOCK-SAT
```

No dependencies to install—uses Python standard library only.

## Usage

### Basic Run

Run a simple SAT solver instance:
```bash
python3 main.py
```

### Example: Ladder Sweep

Run a phase transition sweep across multiple clause-to-variable ratios:
```bash
python3 main.py --door PHASE --planets 4 --secs 6 --ladder 3.30,4.50,4.80,4.90 --trials 3
```

### Command-Line Arguments

- `--door` (default: `PHASE`): Search mode
  - `PHASE`: Phase transition analysis mode
  
- `--planets` (default: 4): Number of parallel solver instances  
  
- `--secs` (default: 6): Seconds per trial  
  
- `--ladder` (default: `4.26`): Comma-separated list of clause-to-variable ratios to test  
  
- `--trials` (default: 1): Number of trials per ratio  
  
- `--seed` (default: random): Random seed for reproducibility  
  
- `--log`: Enable CSV logging to temp directory  
  
- `--verbose`: Enable verbose output

### Example: Multiple Configurations

Run with custom settings:
```bash
python3 main.py --planets 8 --secs 10 --ladder 4.0,4.2,4.26,4.3,4.5 --trials 5 --log --verbose
```

## Output

### Console Output
- Real-time statistics for each trial
- Solvability results (SAT/UNSAT)
- Solution statistics

### CSV Logging (with --log)
When logging is enabled, the solver writes to:
- `{temp_dir}/phaselock_sat.csv`

Contains fields for:
- Timestamp
- Ratio (clause-to-variable)
- Trial number
- Planet instance
- Search statistics
- Solution status

## Architecture

### Planet System
- Each "planet" is an independent local search instance
- Planets share a global best-known solution via thread-safe state
- Implements GSAT-style random walk heuristics
- Periodic random restarts to escape local minima

### Phase Transition
The 3-SAT phase transition occurs around a clause-to-variable ratio of ~4.26:
- **Below 4.26**: Most instances are satisfiable (SAT region)
- **Above 4.26**: Most instances are unsatisfiable (UNSAT region)
- **Near 4.26**: Maximum difficulty for SAT solvers

## Performance Tips

1. **Increase planets** for harder instances (more parallel search)
2. **Increase secs** for longer search times per trial
3. **Use ladder sweeps** to systematically explore phase behavior
4. **Enable logging** to analyze solver behavior over time

## Logging and Analysis

Example: Save logs for analysis
```bash
python3 main.py --planets 4 --secs 10 --ladder 3.5,4.0,4.26,4.5,5.0 --trials 5 --log
```

Then analyze the CSV output:
```python
import pandas as pd
df = pd.read_csv('path/to/phaselock_sat.csv')
# Plot phase behavior by ratio
```

## Experimental Status

⚠️ **This is experimental code**. It's designed for:
- Phase transition exploration
- SAT solver algorithm research
- Mobile/resource-constrained environments

Not recommended for production SAT solving. For serious SAT problems, use mature solvers like:
- [CaDiCaL](https://github.com/arminbiere/cadical)
- [MapleSAT](http://www.maplesat.ca/)

## Technical Details

### Mobile Optimization
- Single-file design for easy deployment
- Uses standard library only (no pip install needed)
- Temp directory for logs (automatically cleaned)
- Minimal memory footprint

### Algorithm
- GSAT-based local search with random walk
- Random restart strategy
- Shared best-known solution across planets
- Clause selection via fitness function

## Contributing

Contributions welcome! Please feel free to:
- Submit issues for bugs or feature requests
- Create pull requests with improvements
- Share phase transition analysis results

## License

This project is experimental research code. See LICENSE file for details.

## References

- **3-SAT Phase Transition**: Cheeseman, P., Kanefsky, B., & Taylor, W. M. (1991). "Where the Really Hard Problems Are"
- **GSAT Algorithm**: Selman, B., Levesque, H. J., & Mitchell, D. G. (1992). "A new method for solving hard satisfiability problems"

## Contact

For questions about this experimental SAT solver, please open an issue on GitHub.

---

**Last Updated**: 2026-02-23
# Anson PHASELOCK-SAT (Mobile Build)

## The Universal Solver Governance
A high-efficiency 3-SAT solver designed for supercritical regimes (Ratio 3.3 to 9.0). This build treats logic as a mechanical lock and variables as pins.

### Key Logic:
- **Simplicial Aperture:** Contradiction cores form a triangulated mesh window.
- **3-6-9 Harmonic Law:** - **Small 9:** Singularity lift for high-pressure pins ($P > 10^5$).
  - **Medium 6:** Stability for mid-range gate pins ($800 < P < 900$).
  - **Big 3:** Grounding for the foundational population.
- **Problem-Solution Summation:** The pressure of one variable is the key to the next.

### Execution Status:
- **Resonance Reached:** Ratio 3.30, 4.80, 4.90 -> `best_unsat=0`.
- **Environment:** iOS/Linux Mobile Build (Lubuntu/Thin-OS recommended).
