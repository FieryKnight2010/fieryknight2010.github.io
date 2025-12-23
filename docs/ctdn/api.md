# CTDN API Reference

Python API documentation for CTDN.

---

## Model

### `CTDN`

Main model class for Causal Temporal Diffusion Networks.

```python
from src.model import CTDN

model = CTDN(
    n_genes: int = 978,
    hidden_dim: int = 256,
    n_heads: int = 8,
    n_timesteps: int = 10,
    lstm_hidden: int = 128,
    lstm_layers: int = 2,
    dropout: float = 0.3
)
```

**Parameters:**

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `n_genes` | int | 978 | Number of input genes |
| `hidden_dim` | int | 256 | Hidden layer dimension |
| `n_heads` | int | 8 | Number of attention heads |
| `n_timesteps` | int | 10 | Diffusion timesteps |
| `lstm_hidden` | int | 128 | LSTM hidden dimension |
| `lstm_layers` | int | 2 | Number of LSTM layers |
| `dropout` | float | 0.3 | Dropout rate |

**Methods:**

```python
# Forward pass
output = model(x)  # x: (batch_size, n_genes)

# Get causal adjacency matrix
adj_matrix = model.get_causal_adjacency()

# Get diffusion embeddings
embeddings = model.get_diffusion_embeddings(x)
```

---

## Training

### `train_model`

Train the CTDN model.

```python
from src.train import train_model

results = train_model(
    model: CTDN,
    data: dict,
    batch_size: int = 32,
    epochs: int = 100,
    learning_rate: float = 0.001,
    weight_decay: float = 1e-4,
    use_focal_loss: bool = True,
    focal_alpha: float = 0.75,
    focal_gamma: float = 2.0,
    class_weights: dict = {0: 1.0, 1: 11.0},
    early_stop_patience: int = 20,
    device: str = 'auto'
)
```

**Returns:**

```python
{
    'train_losses': List[float],
    'val_losses': List[float],
    'val_aurocs': List[float],
    'best_epoch': int,
    'best_auroc': float
}
```

---

## Data Loading

### `load_data`

Load dataset from directory.

```python
from src.data import load_data

data = load_data(data_dir: str)
```

**Returns:**

```python
{
    'gene_expressions': np.ndarray,  # (n_samples, n_genes)
    'efficacy_labels': np.ndarray,   # (n_samples,)
    'train_idx': np.ndarray,
    'test_idx': np.ndarray,
    'drug_names': List[str],
    'test_aeds': List[str]
}
```

### `generate_simulated_data`

Generate simulated dataset.

```python
from src.data import generate_simulated_data

data = generate_simulated_data(
    n_samples: int = 3000,
    n_genes: int = 978,
    n_positive: int = 248,
    random_state: int = 2024
)
```

---

## Evaluation

### `evaluate_model`

Evaluate model on test set.

```python
from src.evaluate import evaluate_model

metrics = evaluate_model(
    model: CTDN,
    data: dict,
    threshold: float = 0.5
)
```

**Returns:**

```python
{
    'auroc': float,
    'auprc': float,
    'precision_at_10': float,
    'precision_at_20': float,
    'recall_at_100': float,
    'predictions': np.ndarray,
    'true_labels': np.ndarray
}
```

---

## Utilities

### `FocalLoss`

Focal loss for class imbalance.

```python
from src.train import FocalLoss

criterion = FocalLoss(alpha=0.75, gamma=2.0)
loss = criterion(predictions, targets)
```

### `WeightedSampler`

Weighted sampler for balanced batches.

```python
from src.data import WeightedSampler

sampler = WeightedSampler(
    labels: np.ndarray,
    class_weights: dict = {0: 1.0, 1: 11.0}
)
```
