# CTDN Quick Start

Get up and running with CTDN in minutes.

---

## Installation

```bash
# Clone the repository
git clone https://github.com/fieryknight2010/ctdn.git
cd ctdn

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install package in development mode
pip install -e .
```

---

## Generate Data

Since the original LINCS L1000 data files are large (>500MB), we provide a script to generate simulated data with the same characteristics:

```bash
python scripts/generate_data.py --output data/ --n_samples 3000 --n_genes 978
```

This will create:

- `data/gene_expressions.npy` - Gene expression profiles (3000, 978)
- `data/efficacy_labels.npy` - Binary efficacy labels (3000,)
- `data/train_idx.npy` - Training indices
- `data/test_idx.npy` - Test indices
- `data/drug_names.csv` - Drug names
- `data/test_aeds.csv` - Test AED names

!!! note
    If you have access to real LINCS L1000 data, place the files in the `data/` directory with the same names.

---

## Train Model

```bash
# Train CTDN with default hyperparameters
python scripts/train_ctdn.py

# Train with custom hyperparameters
python scripts/train_ctdn.py --hidden_dim 256 --n_heads 8 --batch_size 32 --epochs 100
```

**Training outputs:**

- Model checkpoints saved to `results/checkpoints/`
- Training logs saved to `results/logs/`
- Best model saved as `results/best_ctdn_model.pth`

---

## Evaluate Model

```bash
# Evaluate best model on test set
python scripts/evaluate_ctdn.py --model_path results/best_ctdn_model.pth

# Generate predictions
python scripts/evaluate_ctdn.py --model_path results/best_ctdn_model.pth --output results/predictions.csv
```

---

## Compare with Baselines

```bash
# Compare CTDN with baseline methods
python scripts/compare_methods.py
```

This will compare:

- CTDN (your model)
- MGAN-DR
- Random Forest
- Connectivity Map
- Lv et al. 2024

---

## Python API

```python
from src.model import CTDN
from src.train import train_model
from src.data import load_data

# Load data
data = load_data('data/')

# Initialize model
model = CTDN(
    n_genes=978,
    hidden_dim=256,
    n_heads=8,
    n_timesteps=10,
    dropout=0.3
)

# Train
results = train_model(
    model=model,
    data=data,
    batch_size=32,
    epochs=100,
    learning_rate=0.001,
    use_focal_loss=True,
    class_weights={0: 1.0, 1: 11.0}
)

# Save
import torch
torch.save(model.state_dict(), 'my_ctdn_model.pth')
```

---

## Testing

Run unit tests:

```bash
# Run all tests
pytest tests/

# Run specific test file
pytest tests/test_model.py

# Run with coverage
pytest --cov=src tests/
```
