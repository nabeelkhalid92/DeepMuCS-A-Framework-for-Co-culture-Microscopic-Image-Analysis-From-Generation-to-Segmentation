# DeepMuCS-A-Framework-for-Co-culture-Microscopic-Image-Analysis-From-Generation-to-Segmentation

![Framework Diagram](images/framework_diagram.png)

Discrimination between cell types in the co-culture environment with multiple cell lines can assist in examining the interaction between different cell populations. Identifying different cell cultures in addition to cell segmentation in co-culture is essential for understanding the cellular mechanisms associated with disease states. In drug development, biologists are more interested in co-culture models because they replicate the tumor environment in vivo better than the monoculture models. Additionally, they have a measurable effect on cancer cell response to treatment. Co-culture models are critical for designing a drug with maximum efficacy on cancer while minimizing harm to the rest of the body.

In the past, there existed minimal progress related to cell-type aware segmentation in the monoculture and no development whatsoever for the co-culture. The introduction of the LIVECell dataset has allowed us to perform experiments for cell-type-aware segmentation. However, it is composed of microscopic images in a monoculture environment. This paper presents a framework for co-culture microscopic image data generation, where each image can contain multiple cell cultures. The framework also presents a pipeline for culture-dependent cell segmentation in co-culture microscopic images. The extensive evaluation revealed that it is possible to achieve cell-type aware segmentation in co-culture microscopic images with good precision.

## Features

- Generation of co-culture microscopic images with multiple cell types.
- Culture-dependent cell segmentation pipeline.
- Evaluation metrics for precision in cell-type aware segmentation.

## Installation

### DeepMuCS Installation

Do not install the original detectron2 as it conflicts with the ResNeSt code. If it is already installed, uninstall it or create a new virtual environment.

1. Clone and install detectron2-ResNeSt:
    ```bash
    git clone https://github.com/chongruo/detectron2-ResNeSt
    python -m pip install -e detectron2-ResNeSt
    ```

For further information on installation and usage, see the [detectron2-ResNeSt documentation](https://github.com/chongruo/detectron2-ResNeSt).

### Common Installation Issues

If you encounter issues like "Not compiled with GPU support" or "Detectron2 CUDA Compiler: not available," ensure CUDA is properly installed:
```bash
python -c 'import torch; from torch.utils.cpp_extension import CUDA_HOME; print(torch.cuda.is_available(), CUDA_HOME)'

This should print valid outputs confirming CUDA availability.

## Data

You can download the dataset from the following link:

[DeepMuCS Dataset Download](https://cloud.dfki.de/owncloud/index.php/s/ZRFRjQgmxo8ocqp)

## Usage

### Register LIVECell Dataset

Register the dataset via the detectron2 Python API by adding the following code to the `train_net.py` file:

```python
from detectron2.data.datasets import register_coco_instances
register_coco_instances("dataset_name", {}, "/path/coco/annotations.json", "path/to/image/dir")
