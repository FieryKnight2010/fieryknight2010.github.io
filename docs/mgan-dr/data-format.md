# MGAN-DR Data Format

Specifications for input and output data formats.

---

## Input Data

### Gene Expression Matrix

**File**: `gene_expressions.npy`

| Property | Value |
|----------|-------|
| Shape | `(n_samples, n_genes)` |
| Format | NumPy array, float32 |
| Normalization | Z-score normalized per gene |
| Example | `(3000, 978)` |

### Efficacy Labels

**File**: `efficacy_labels.npy`

| Property | Value |
|----------|-------|
| Shape | `(n_samples,)` |
| Format | NumPy array, int |
| Values | 0 (non-AED) or 1 (AED) |
| Class distribution | ~8.3% positive (11:1 imbalance) |

### Train/Test Indices

- `train_idx.npy`: Training sample indices
- `test_idx.npy`: Test sample indices
- Stratified split maintaining class balance

---

## Data Generation

If you don't have the real data, our simulation script generates realistic data with:

1. **Biological signal**: Positive samples have elevated expression in epilepsy-related pathways
2. **Class imbalance**: 11:1 negative:positive ratio (matching real data)
3. **Feature correlations**: Realistic gene-gene correlations
4. **Multiple samples per drug**: Multiple measurements per compound

### Using the Data Generation Script

```bash
python scripts/generate_data.py --output data/ --n_samples 3000 --n_genes 978
```

### Using the Python API

```python
from src.data import generate_simulated_data

# Generate 3000 samples with 978 genes
data_dict = generate_simulated_data(
    n_samples=3000,
    n_genes=978,
    n_positive=248,  # 8.3% positive rate
    random_state=2024
)

# Save to disk
import numpy as np
np.save('data/gene_expressions.npy', data_dict['gene_expressions'])
np.save('data/efficacy_labels.npy', data_dict['efficacy_labels'])
np.save('data/train_idx.npy', data_dict['train_idx'])
np.save('data/test_idx.npy', data_dict['test_idx'])
```

---

## Output Data

### Predictions

**File**: `predictions.csv`

| Column | Description |
|--------|-------------|
| `drug_name` | Name of the drug |
| `prediction` | Model probability (0-1) |
| `true_label` | Ground truth label (0 or 1) |

### Model Checkpoints

**Directory**: `results/checkpoints/`

- `model_epoch_XX.pth` - Model state at epoch XX
- `best_model.pth` - Best model based on validation AUROC

### Training Logs

**Directory**: `results/logs/`

- `training.log` - Training metrics per epoch
- `tensorboard/` - TensorBoard logs (if enabled)
