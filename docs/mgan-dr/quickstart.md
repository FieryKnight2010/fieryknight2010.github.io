# MGAN-DR Quick Start

Get up and running with MGAN-DR in minutes.

---

## Installation

```bash
# Clone the repository
git clone https://github.com/fieryknight2010/mgan-dr.git
cd mgan-dr

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

Since the original data files are large (>500MB), we provide a script to generate simulated data with the same characteristics:

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
    If you have access to the real dataset, place the files in the `data/` directory with the same names.

---

## Train Model

```bash
# Train MGAN-DR with default hyperparameters
python scripts/train_mgan.py

# Train with custom hyperparameters
python scripts/train_mgan.py --hidden_dims 512 256 128 --batch_size 32 --epochs 150
```

**Training outputs:**

- Model checkpoints saved to `results/checkpoints/`
- Training logs saved to `results/logs/`
- Best model saved as `results/best_model.pth`

---

## Evaluate Model

```bash
# Evaluate best model on test set
python scripts/evaluate_mgan.py --model_path results/best_model.pth

# Generate predictions
python scripts/evaluate_mgan.py --model_path results/best_model.pth --output results/predictions.csv
```

---

## Compare with Baselines

```bash
# Compare MGAN-DR with baseline methods
python scripts/compare_baselines.py
```

This will compare:

- MGAN-DR (your model)
- Random Forest
- Connectivity Map
- Tau Scoring
- Lv et al. 2024

---

## Python API

```python
from src.model import MGANDR
from src.train import train_model
from src.data import load_data

# Load data
data = load_data('data/')

# Initialize model
model = MGANDR(
    input_dim=978,
    hidden_dims=[512, 256, 128],
    dropout_rates=[0.4, 0.3, 0.2]
)

# Train
results = train_model(
    model=model,
    data=data,
    batch_size=32,
    epochs=150,
    learning_rate=0.001,
    use_focal_loss=True,
    class_weights={0: 1.0, 1: 11.0}
)

# Save
import torch
torch.save(model.state_dict(), 'my_model.pth')
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
