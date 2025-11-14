# PyNN Example - Motoneuron Pool Simulation

This repository contains a minimal example of using PyNN to simulate a pool of motoneurons with custom ion channels implemented in NEURON.

## Overview

The project demonstrates:
- Creating custom ion channel models (Na, Kf, Ks) using PyNN's `StandardIonChannelModel`
- Building multi-compartment neurons with soma and dendrite
- Simulating a population of 100 motoneurons with varying biophysical properties
- Recording and visualizing membrane potential, gating variables, and spike trains

## Prerequisites

- Python 3.10, 3.11, or 3.12
- [uv](https://github.com/astral-sh/uv) - A fast Python package installer and resolver

## Installation

### 1. Install uv

If you don't have `uv` installed, you can install it using:

```bash
# On macOS and Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# On Windows
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"

# Or using pip
pip install uv
```

### 2. Set up the project

Clone the repository and navigate to the project directory:

```bash
git clone <repository-url>
cd pynn_example
```

### 3. Create a virtual environment and install dependencies

Using `uv`, create a virtual environment and install all dependencies defined in `pyproject.toml`:

```bash
# Create virtual environment and install dependencies
uv sync
```

This command will:
- Create a `.venv` directory with a Python virtual environment
- Install all dependencies listed in `pyproject.toml`
- Generate/update the `uv.lock` file for reproducible builds

### 4. Activate the virtual environment

```bash
# On Linux/macOS
source .venv/bin/activate

# On Windows
.venv\Scripts\activate
```

## Running the Example

### Using Jupyter Notebook

1. Start Jupyter Notebook:

```bash
jupyter notebook
```

2. Open `example.ipynb` in your browser

3. Run the cells sequentially

### What the Example Does

The `example.ipynb` notebook demonstrates the following workflow:

#### 1. **NMODL Compilation** (Cells 1-2)
- Imports necessary PyNN and NEURON modules
- Copies the custom `mn.mod` file (motoneuron model) to the PyNN NEURON directory
- Compiles the NMODL file and loads it into NEURON

#### 2. **Custom Ion Channel Definitions** (Cells 3-6)
- **KsChannel**: Slow potassium channel with gating variable `p`
- **KfChannel**: Fast potassium channel with gating variable `n`
- **NaChannel**: Sodium channel with gating variables `m` and `h`
- **PassiveLeak**: Passive leak conductance

#### 3. **Multi-Compartment Neuron Class** (Cell 7)
- Defines `mn_class` that inherits from `sim.MultiCompartmentNeuron`
- Integrates all custom ion channels
- Defines recordable variables and units

#### 4. **Morphology Creation** (Cells 8-9)
- Creates 100 neurons with varying soma and dendrite dimensions
- Each neuron has a two-compartment structure (soma + dendrite)
- Morphological parameters vary linearly across the population

#### 5. **Neuron Configuration** (Cell 10)
- Sets membrane capacitance and axial resistance
- Configures ion channel distributions and parameters
- Applies different voltage thresholds (`vt`) across the population (-57.65 to -53 mV)

#### 6. **Population and Stimulation** (Cells 11-12)
- Creates a population of 100 motoneurons
- Injects a DC current (200 nA) into the dendrites for 100 ms

#### 7. **Recording** (Cell 13)
- Records spike times for all neurons
- Records membrane potential at soma and dendrite for neurons 0 and 50
- Records gating variables (m, h, n, p) at the soma for neurons 0 and 50

#### 8. **Simulation** (Cell 14)
- Runs the simulation for 100 ms

#### 9. **Visualization** (Cell 15)
- Plots membrane potential, gating variables, and spike raster
- Saves the figure as `teste.png`

## Project Structure

```
pynn_example/
├── example.ipynb      # Main Jupyter notebook with the simulation
├── mn.mod             # NEURON NMODL file defining motoneuron ion channels
├── pyproject.toml     # Project dependencies and metadata
├── uv.lock            # Lock file for reproducible dependency installation
├── test.png           # Example output figure
└── README.md          # This file
```

## Dependencies

The project uses the following main dependencies (defined in `pyproject.toml`):

- **PyNN**: Python package for simulator-independent neural network modeling
- **NEURON**: Simulation environment for biophysically detailed neurons
- **NumPy**: Numerical computing library
- **Matplotlib**: Plotting library
- **Jupyter**: Interactive notebook environment
- **PyNeuroML**: Tools for working with NeuroML morphologies

## Using uv for Package Management

### Adding new dependencies

```bash
uv add <package-name>
```

### Removing dependencies

```bash
uv remove <package-name>
```

### Updating dependencies

```bash
uv sync --upgrade
```

### Running Python scripts without activating the environment

```bash
uv run python script.py
```

### Running Jupyter without activating the environment

```bash
uv run jupyter notebook
```

## Troubleshooting

### NMODL compilation issues

If you encounter issues with NMODL compilation, ensure that:
- NEURON is properly installed with the `nrnivmodl` compiler
- The path to the `.venv` directory in cell 2 matches your Python version

### Import errors

If you get import errors, make sure you've activated the virtual environment or use `uv run` to execute commands.

## License

This project is licensed under the GNU General Public  License.

## Contact

renato.watanabe@ufabc.edu.br

