# DeepMuCS-A-Framework-for-Co-culture-Microscopic-Image-Analysis-From-Generation-to-Segmentation

![Framework Diagram](images/framework_diagram.png)

Discrimination between cell types in the co-culture environment with multiple cell lines can assist in examining the interaction between different cell populations. Identifying different cell cultures in addition to cell segmentation in co-culture is essential for understanding the cellular mechanisms associated with disease states. In drug development, biologists are more interested in co-culture models because they replicate the tumor environment in vivo better than the monoculture models. Additionally, they have a measurable effect on cancer cell response to treatment. Co-culture models are critical for designing a drug with maximum efficacy on cancer while minimizing harm to the rest of the body.

In the past, there existed minimal progress related to cell-type aware segmentation in the monoculture and no development whatsoever for the co-culture. The introduction of the LIVECell dataset has allowed us to perform experiments for cell-type-aware segmentation. However, it is composed of microscopic images in a monoculture environment. This paper presents a framework for co-culture microscopic image data generation, where each image can contain multiple cell cultures. The framework also presents a pipeline for culture-dependent cell segmentation in co-culture microscopic images. The extensive evaluation revealed that it is possible to achieve cell-type aware segmentation in co-culture microscopic images with good precision.

# Data

You can download the dataset from the following link:

[DeepMuCS Dataset Download](https://cloud.dfki.de/owncloud/index.php/s/ZRFRjQgmxo8ocqp)

The above link contains the data used for training, validation and testing of DeepMuCS800, DeepMuCS1600, DeepMuCS4000.

Here are some characteristics of the data:

## Summary statistics of images and cell instances in the synthetic co-culture training subsets, validation, and test sets.
| **Dataset**       | **Images** | **Total Cells** | **A172** | **BT-474** | **BV-2** | **Huh7** | **MCF7** | **SH-SY5Y** | **SkBr3** | **SK-OV-3** |
|-------------------|------------|-----------------|----------|------------|----------|----------|----------|-------------|-----------|-------------|
| **DeepMuCS800**   | 800        | 10137           | 341      | 982        | 759      | 125      | 1207     | 3630        | 2926      | 167         |
| **DeepMuCS1600**  | 1600       | 19826           | 668      | 1998       | 1402     | 254      | 2347     | 6984        | 5808      | 365         |
| **DeepMuCS4000**  | 4000       | 49613           | 1657     | 4732       | 3482     | 603      | 6031     | 17772       | 14438     | 898         |
| **DeepMuCS_val**  | 570        | 7120            | 227      | 667        | 523      | 101      | 875      | 2519        | 2092      | 116         |
| **DeepMuCS_test** | 1564       | 19408           | 639      | 1843       | 1348     | 246      | 2388     | 6952        | 5668      | 324         |


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
```
This should print valid outputs confirming CUDA availability.

## Training and evaluation

### Register LIVECell Dataset

Register the dataset via the detectron2 Python API by adding the following code to the `train_net.py` file:

```python
from detectron2.data.datasets import register_coco_instances
register_coco_instances("dataset_name", {}, "/path/coco/annotations.json", "path/to/image/dir")
```
Where dataset_name will be the name of your dataset and will be how you decide what dataset to use in your config file. Per default, the config file will point to TRAIN and TEST, so registering a test dataset as TEST will work directly with the provided config files, for other names, make sure to update your config file accordingly.

In the config file change the dataset entries with the name used to register the dataset.
Set the output directory in the config file to save the models and results.
### Train

### Register LIVECell Dataset
Using a custom dataset such as LIVECell together with the detectron2 code base is done by first registering the dataset via the detectron2 Python API. In practice, this can be done by adding the following code to the `train_net.py` file in the cloned centermask2 repo:
To train a model, change the OUTPUT directory in the config file to where the models and checkpoints should be saved. Make sure you follow the previous step and register a TRAIN and TEST dataset, cd into the cloned directory (centermask2 or detectron2-ResNeSt), and run the following code:
```python
python tools/train_net.py --num-gpus 8  --config-file your_config.yaml
```
To fine-tune a model on your own dataset, set MODEL.WEIGTS in the config file to point at one of our weight files, if you want to finetune our centermask2 model for instance.
```bash
MODEL:
  WEIGHTS: "http://livecell-dataset.s3.eu-central-1.amazonaws.com/LIVECell_dataset_2021/models/Anchor_free/ALL/LIVECell_anchor_free_model.pth"
```
