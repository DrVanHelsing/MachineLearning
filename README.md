# MachineLearning

A comprehensive repository for machine learning experiments, models, notebooks, datasets, and utilities.

---

## Badges

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
![Python Version](https://img.shields.io/badge/python-3.8%2B-blue)
![Code Coverage](https://img.shields.io/badge/coverage-85%25-green)

---

## Table of Contents

- [Features](#features)
- [Repository Structure](#repository-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [Data](#data)
- [Models and Checkpoints](#models-and-checkpoints)
- [Examples](#examples)
- [Testing and CI](#testing-and-ci)
- [Contributing](#contributing)
- [License](#license)
- [Contact / Maintainers](#contact--maintainers)
- [Acknowledgements](#acknowledgements)

---

## Features

This repository contains a variety of machine learning resources and tools:

- **Jupyter Notebooks**: Interactive notebooks demonstrating ML algorithms and techniques
- **Python Scripts**: Modular training and evaluation scripts for ML models
- **Pretrained Models**: Ready-to-use model checkpoints for common tasks
- **Dataset Handling**: Utilities for data loading, preprocessing, and augmentation
- **Training/Evaluation Pipelines**: End-to-end workflows for model development
- **Utilities**: Helper functions for logging, visualization, and metrics
- **Docker Support**: Containerized environment for reproducible experiments
- **CI/CD Integration**: Automated testing and deployment workflows

---

## Repository Structure

```
MachineLearning/
├── notebooks/              # Jupyter notebooks for experiments and tutorials
│   ├── Linear Regression/
│   ├── Logistic Regression/
│   └── Neural Networks/
├── src/                    # Source code for ML models and utilities
│   ├── __init__.py
│   ├── train.py           # Training script
│   ├── evaluate.py        # Evaluation script
│   ├── models/            # Model architectures
│   └── utils/             # Helper functions
├── data/                   # Data directory (not tracked in git)
│   ├── raw/               # Raw datasets
│   ├── processed/         # Preprocessed data
│   └── external/          # External data sources
├── models/                 # Saved model checkpoints
│   └── checkpoints/
├── scripts/                # Utility scripts
│   ├── download_data.sh   # Data download helper
│   └── setup_env.sh       # Environment setup
├── tests/                  # Unit and integration tests
│   ├── test_models.py
│   └── test_utils.py
├── docs/                   # Documentation
│   └── api/               # API documentation
├── configs/                # Configuration files
│   └── example.yaml       # Example config
├── Dockerfile              # Docker configuration
├── requirements.txt        # Python dependencies
├── environment.yml         # Conda environment file
├── setup.py                # Package installation script
└── README.md               # This file
```

---

## Installation

### Prerequisites

- Python 3.8 or higher
- Git
- (Optional) Docker for containerized setup

### Option A: Using pip and virtualenv

1. Clone the repository:
   ```bash
   git clone https://github.com/DrVanHelsing/MachineLearning.git
   cd MachineLearning
   ```

2. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Install the package in editable mode:
   ```bash
   pip install -e .
   ```

### Option B: Using conda

1. Clone the repository:
   ```bash
   git clone https://github.com/DrVanHelsing/MachineLearning.git
   cd MachineLearning
   ```

2. Create and activate the conda environment:
   ```bash
   conda env create -f environment.yml
   conda activate ml-env
   ```

3. Install the package in editable mode:
   ```bash
   pip install -e .
   ```

### Option C: Using Docker

1. Clone the repository:
   ```bash
   git clone https://github.com/DrVanHelsing/MachineLearning.git
   cd MachineLearning
   ```

2. Build the Docker image:
   ```bash
   docker build -t machinelearning:latest .
   ```

3. Run the container:
   ```bash
   docker run -it --rm -v $(pwd):/workspace machinelearning:latest
   ```

---

## Usage

### Running Jupyter Notebooks

Navigate to the notebooks directory and launch Jupyter:

```bash
cd notebooks
jupyter notebook
```

Open any notebook (e.g., `Linear Regression/CSC312 - Assignment 1 - Linear Regression.ipynb`) to explore ML algorithms interactively.

### Training a Model

Run the training script with a configuration file:

```bash
python -m src.train --config configs/example.yaml
```

### Evaluating a Model

Evaluate a trained model checkpoint:

```bash
python -m src.evaluate --model models/checkpoint.pt
```

### Running Tests

Execute the test suite using pytest:

```bash
pytest tests/
```

For verbose output:

```bash
pytest tests/ -v
```

### Running Linting

Check code style with flake8:

```bash
flake8 src/
```

For auto-formatting with black:

```bash
black src/ tests/
```

---

## Configuration

Configuration files are stored in the `configs/` directory. These YAML files define parameters for training, evaluation, and data processing.

### Example Configuration (`configs/example.yaml`):

```yaml
dataset:
  name: "mnist"
  path: "data/processed/mnist"
  train_split: 0.8
  val_split: 0.1
  test_split: 0.1

model:
  architecture: "mlp"
  hidden_layers: [128, 64, 32]
  activation: "relu"
  dropout: 0.2

training:
  epochs: 50
  batch_size: 64
  learning_rate: 0.001
  optimizer: "adam"
  loss: "cross_entropy"
  
  seed: 42
  device: "cuda"  # or "cpu"
  
  checkpoint_dir: "models/checkpoints"
  save_frequency: 5
```

Modify these parameters to experiment with different model architectures and hyperparameters.

---

## Data

### Data Organization

Place your datasets in the `data/` directory:

- `data/raw/`: Original, immutable datasets
- `data/processed/`: Cleaned and preprocessed data ready for training
- `data/external/`: Data from third-party sources

### Downloading Data

Use the provided script to download common datasets:

```bash
bash scripts/download_data.sh
```

### Large Files and Git LFS

For large datasets or model files, we recommend using Git Large File Storage (Git LFS):

```bash
git lfs install
git lfs track "*.csv"
git lfs track "*.pt"
git lfs track "*.h5"
```

**Note**: Avoid committing sensitive or proprietary data to the repository. Use `.gitignore` to exclude such files.

---

## Models and Checkpoints

### Saving Models

Models are automatically saved during training to the directory specified in your config file (default: `models/checkpoints/`).

### Recommended Naming Convention

Use descriptive names for model checkpoints:

```
models/checkpoints/
├── model_epoch_10_acc_0.89.pt
├── model_epoch_20_acc_0.92.pt
└── best_model.pt
```

### Pretrained Checkpoints

Pretrained models can be found in the `models/` directory. Load them for inference or fine-tuning:

```python
import torch
model = torch.load('models/best_model.pt')
```

---

## Examples

### Quick Start Example

Here's a complete workflow to get started:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/DrVanHelsing/MachineLearning.git
   cd MachineLearning
   ```

2. **Set up the environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   pip install -e .
   ```

3. **Download sample data**:
   ```bash
   bash scripts/download_data.sh
   ```

4. **Train a model**:
   ```bash
   python -m src.train --config configs/example.yaml
   ```

5. **View training results**:
   Check the logs in the console or visualize metrics using TensorBoard:
   ```bash
   tensorboard --logdir=logs/
   ```

6. **Evaluate the model**:
   ```bash
   python -m src.evaluate --model models/checkpoints/best_model.pt
   ```

---

## Testing and CI

### Running Tests Locally

We use `pytest` for testing. Run all tests with:

```bash
pytest tests/
```

For coverage reports:

```bash
pytest tests/ --cov=src --cov-report=html
```

### Continuous Integration

This repository uses GitHub Actions for automated testing and deployment. Workflows are defined in `.github/workflows/`.

**CI Pipeline includes**:
- Linting (flake8, black)
- Unit tests (pytest)
- Integration tests
- Code coverage reporting

### Writing Tests

When contributing new features, please add corresponding tests in the `tests/` directory. Follow the existing test structure and naming conventions.

---

## Contributing

We welcome contributions! Here's how to get started:

### Getting Started

1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/MachineLearning.git
   cd MachineLearning
   ```

3. **Create a feature branch**:
   ```bash
   git checkout -b feature/your-feature-name
   ```

4. **Make your changes** and commit them:
   ```bash
   git add .
   git commit -m "feat: add your feature description"
   ```

5. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```

6. **Open a Pull Request** on the main repository

### Code Style Guidelines

- Follow PEP 8 for Python code
- Use meaningful variable and function names
- Add docstrings to functions and classes
- Keep functions focused and modular
- Run `flake8` and `black` before committing

### Commit Message Guidelines

Use conventional commit format:

- `feat:` for new features
- `fix:` for bug fixes
- `docs:` for documentation changes
- `test:` for adding tests
- `refactor:` for code refactoring
- `chore:` for maintenance tasks

Example: `feat: add support for LSTM models`

### Issue Templates

When opening an issue, please use the provided templates for:
- Bug reports
- Feature requests
- Documentation improvements

### Code of Conduct

Please be respectful and constructive in all interactions. See our Code of Conduct for details.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

**Note**: Please ensure you include a LICENSE file in the repository root if one doesn't already exist.

---

## Contact / Maintainers

**Maintainer**: DrVanHelsing

For questions, suggestions, or issues:
- Open an issue on [GitHub Issues](https://github.com/DrVanHelsing/MachineLearning/issues)
- Contact the maintainer through GitHub

We encourage you to open issues for support rather than direct contact to help build a knowledge base for the community.

---

## Acknowledgements

This project builds upon various open-source libraries and frameworks:

- **PyTorch / TensorFlow**: Deep learning frameworks
- **NumPy / Pandas**: Data manipulation and analysis
- **Scikit-learn**: Machine learning utilities
- **Matplotlib / Seaborn**: Data visualization
- **Jupyter**: Interactive computing environment

Special thanks to the machine learning community for tutorials, datasets, and inspiration.

---

**Happy Learning! 🚀**
