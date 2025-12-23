# MGAN-DR API Reference

Python API documentation for MGAN-DR.

---

## Model

### `MGANDR`

Main model class for Multi-Modal Graph Attention Network for Drug Repurposing.

```python
from src.model import MGANDR

model = MGANDR(
    input_dim: int = 978,
    hidden_dims: List[int] = [512, 256, 128],
    dropout_rates: List[float] = [0.4, 0.3, 0.2],
    n_attention_heads: int = 4
)
```

**Parameters:**

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `input_dim` | int | 978 | Number of input genes |
| `hidden_dims` | List[int] | [512, 256, 128] | Hidden layer dimensions |
| `dropout_rates` | List[float] | [0.4, 0.3, 0.2] | Dropout rates per layer |
| `n_attention_heads` | int | 4 | Number of attention heads |

**Methods:**

```python
# Forward pass
output = model(x)  # x: (batch_size, n_genes)

# Get attention weights
attention_weights = model.get_attention_weights(x)

# Get intermediate representations
embeddings = model.get_embeddings(x, layer=2)
```

---

## Training

### `train_model`

Train the MGAN-DR model.

```python
from src.train import train_model

results = train_model(
    model: MGANDR,
    data: dict,
    batch_size: int = 32,
    epochs: int = 150,
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
    model: MGANDR,
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

### `GraphAttentionLayer`

Graph attention layer component.

```python
from src.model import GraphAttentionLayer

gat = GraphAttentionLayer(
    in_features: int = 512,
    out_features: int = 256,
    n_heads: int = 4,
    dropout: float = 0.3
)
```
