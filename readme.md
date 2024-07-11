# DeepMuCS-A-Framework-for-Co-culture-Microscopic-Image-Analysis-From-Generation-to-Segmentation

![Framework Diagram](images/framework_diagram.png)

Discrimination between cell types in the co-culture environment with multiple cell lines can assist in examining the interaction between different cell populations. Identifying different cell cultures in addition to cell segmentation in co-culture is essential for understanding the cellular mechanisms associated with disease states. In drug development, biologists are more interested in co-culture models because they replicate the tumor environment in vivo better than the monoculture models. Additionally, they have a measurable effect on cancer cell response to treatment. Co-culture models are critical for designing a drug with maximum efficacy on cancer while minimizing harm to the rest of the body.

In the past, there existed minimal progress related to cell-type aware segmentation in the monoculture and no development whatsoever for the co-culture. The introduction of the LIVECell dataset has allowed us to perform experiments for cell-type-aware segmentation. However, it is composed of microscopic images in a monoculture environment. This paper presents a framework for co-culture microscopic image data generation, where each image can contain multiple cell cultures. The framework also presents a pipeline for culture-dependent cell segmentation in co-culture microscopic images. The extensive evaluation revealed that it is possible to achieve cell-type aware segmentation in co-culture microscopic images with good precision.

## Features

- Generation of co-culture microscopic images with multiple cell types.
- Culture-dependent cell segmentation pipeline.
- Evaluation metrics for precision in cell-type aware segmentation.

## Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/DeepMuCS.git
    ```
2. Navigate to the project directory:
    ```bash
    cd DeepMuCS
    ```
3. Install the required dependencies:
    ```bash
    pip install -r requirements.txt
    ```

## Usage

1. Prepare your input images and place them in the `input_images` directory.
2. Run the image generation pipeline:
    ```bash
    python generate_images.py
    ```
3. Perform cell segmentation on the generated images:
    ```bash
    python segment_cells.py
    ```

## Example

Here is an example of how to run the framework:
```bash
python main.py --input_dir path/to/input_images --output_dir path/to/output_images
