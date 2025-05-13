# PyMC Installation and Testing Process

## Repository Setup
1. Clone the repository
```bash
cd /tmp && git clone https://github.com/pymc-devs/pymc.git
```
Purpose: Download the PyMC source code from GitHub
Result: Successfully cloned the repository

## Environment Setup
1. Create and activate virtual environment
```bash
cd /tmp/pymc
python3 -m venv venv
source venv/bin/activate
```
Purpose: Create an isolated Python environment for the project
Result: Successfully created virtual environment

2. Install development dependencies
```bash
pip install -r requirements-dev.txt
```
Purpose: Install all required development dependencies
Result: Successfully installed development dependencies

## Testing Process
1. Initial test attempt
```bash
python -m pytest tests/
```
Purpose: Run the test suite
Result: Failed due to missing JAX dependency

2. Install JAX
```bash
pip install "jax[cpu]"
```
Purpose: Install JAX for CPU computations
Result: Successfully installed JAX and its dependencies

3. Install NumPyro
```bash
pip install numpyro
```
Purpose: Install NumPyro for JAX-based probabilistic programming
Result: Successfully installed NumPyro

4. Run full test suite
```bash
python -m pytest tests/
```
Purpose: Run the complete test suite with all dependencies
Result: Test execution in progress (takes significant time to complete)

## Project Structure
The repository contains the following key components:
- `pymc/`: Main package directory
- `tests/`: Test suite
- `docs/`: Documentation
- `requirements.txt`: Basic requirements
- `requirements-dev.txt`: Development requirements
- `pyproject.toml`: Project configuration
- `setup.py`: Installation script

## Notes
- The project requires several key dependencies including JAX and NumPyro for certain functionalities
- Test suite is extensive with over 3,600 test cases
- Some tests may require significant computational resources and time to complete
- The project uses pytest as its testing framework

## Dependencies Installed
- Python development tools
- JAX (CPU version)
- NumPyro
- Various development dependencies from requirements-dev.txt
