# Shape Completion Toolkit

To speed up the usage of our dataset, we provide a development kit providing a PyTorch-based data loader and a small library for computing the metrics that we use in
the challenge relative to this dataset.

## Dataloader

```python
from torch.utils.data import DataLoader
from dataloader import ShapeCompletionDataset

shape_completion_dataset = ShapeCompletionDataset(data_source='path_to_data/')
dataloader = DataLoader(shape_completion_dataset)

for item in dataloader:
    <do stuff>

```

## Metrics

```python
import open3d as o3d

from chamfer_distance import ChamferDistance
from precision_recall import PrecisionRecall

cd = ChamferDistance()
pr = PrecisionRecall(min_t=0.001,max_t=0.01,num=10)

# list of prediction and corresponding groundtruth
predictions = [...]
groundtruths = [...]

for prediction, groundtruth in zip(predictions,groundtruths):

    cd.update(groundtruth, prediction)  
    pr.update(groundtruth, prediction)  

final_cd_metric = cd.compute()
final_pr_metrics = pr.compute()

cd.reset()
pr.reset()
```
