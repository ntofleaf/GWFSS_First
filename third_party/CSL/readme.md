# CSL

## 🚀 Project Overview

CSL (Confidence Separable Learning) is a research project dedicated to advancing semi-supervised semantic segmentation. This codebase provides the official implementation for the paper "When Confidence Fails: Revisiting Pseudo-Label Selection in Semi-supervised Semantic Segmentation" (ICCV 2025).

This project addresses a critical limitation in existing pseudo-labeling methods for semi-supervised semantic segmentation: their typical reliance on fixed confidence thresholds. Such methods often struggle with network overconfidence, leading to overlapping high-confidence regions for both correct and incorrect predictions, which amplifies model cognitive bias. Furthermore, directly discarding low-confidence predictions can disrupt spatial-semantic continuity and result in significant context loss.

CSL proposes a novel approach that formulates pseudo-label selection as a convex optimization problem within the confidence distribution, enabling a more robust and adaptive selection strategy. By doing so, CSL aims to overcome the challenges of overconfidence and context loss, ultimately enhancing the performance of semi-supervised semantic segmentation models.

This repository includes comprehensive training and evaluation scripts for popular datasets like Pascal VOC and Cityscapes, facilitating easy reproduction of results and further research.
-----

## 🛠️ Getting Started

### Installation

Before you begin, please ensure you have `conda` (or `miniconda`) and `git` installed on your system.

```bash
# Clone the project repository
git clone https://github.com/PanLiuCSU/CSL 
cd CSL

# Create and activate the Conda environment
conda create -n csl python=3.11.9
conda activate csl

# Install project dependencies
pip install -r requirements.txt

# Install PyTorch and TorchVision (select based on your CUDA version)
# Note: The command below installs PyTorch 2.4.0 and TorchVision 0.19.0 with the latest CUDA compatible version.
pip install torch==2.4.0 torchvision==0.19.0 -f https://download.pytorch.org/whl/torch_stable.html

# If you have specific CUDA version requirements, please visit the PyTorch website for the corresponding installation command.
# For example, for CUDA 11.8:
# pip install torch==2.4.0 torchvision==0.19.0 torchaudio==2.4.0 --index-url https://download.pytorch.org/whl/cu118
```

-----

### Dataset Preparation

This project supports the following image segmentation datasets:

  - **Pascal VOC 2012:** ([http://host.robots.ox.ac.uk/pascal/VOC/voc2012/index.html](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/index.html))
  - **Cityscapes:** ([https://www.cityscapes-dataset.com/](https://www.cityscapes-dataset.com/))

Please download and extract the datasets according to their official guidelines. After downloading, you will need to **modify the configuration files in the project (typically located in `configs/` or `data/` directories)** to point to the actual paths of your local datasets.

**Expected Dataset Directory Structure Example:**

```
# Dataset Root Directory (e.g., /data/datasets)
├── [Your Pascal Path] # e.g., /data/datasets/VOCdevkit/VOC2012
│   ├── JPEGImages     # Contains original images
│   └── SegmentationClass # Contains semantic segmentation annotations https://drive.google.com/file/d/1ikrDlsai5QSf2GiSUR3f8PZUzyTubcuF/view
│   └── Annotations (Option) # Optional, original annotation files
│   └── ImageSets (Option)   # Optional, dataset split information
│   └── SegmentationObject (Option) # Optional, instance segmentation annotations
│
├── [Your Cityscapes Path] # e.g., /data/datasets/cityscapes
│   ├── leftImg8bit      # Contains original images
│   └── gtFine           # Contains fine annotations (semantic, instance segmentation, etc.)
```

**Important Note:** Make sure to check and update parameters like `data_root` or `dataset_path` in the relevant configuration files to correctly point to your local dataset paths.

-----

## 🚀 Usage

This project provides two main training modes: Contrastive/Consistency Self-Learning (CSL) and Supervised Baseline. All training scripts are located in the `scripts/` directory.

### 1\. Contrastive/Consistency Self-Learning (CSL) Training

Run the following command to start the training process for the CSL framework. This mode is typically used to learn robust feature representations from large amounts of unlabeled data.

```bash
cd CSL
bash scripts/csl.sh
```

  * **Script Details:** The `csl.sh` script will contain specific commands for training the CSL model, such as selecting the model architecture, optimizer, learning rate scheduler, log output path, etc. Please review the script for detailed configurations.
  * **Configuration Adjustment:** You can adjust training parameters by modifying the `csl.sh` script or the configuration files it references (e.g., `configs/csl_config.yaml` or `models/csl/config.py`, depending on your project structure), such as batch size, number of epochs, self-supervised task weights, etc.

-----

### 2\. Supervised Baseline Training

Run the following command to start training the traditional supervised learning baseline model. This mode trains end-to-end directly on labeled datasets and is used for performance comparison with the CSL method.

```bash
cd CSL
bash scripts/supervised.sh
```

  * **Script Details:** The `supervised.sh` script will invoke commands for training the supervised model, which may include different model backbones, loss functions, data augmentation strategies, etc.
  * **Configuration Adjustment:** Similar to CSL, you can adjust supervised training parameters by modifying the `supervised.sh` script or the configuration files it references (e.g., `configs/supervised_baseline.yaml` or `models/supervised/config.py`).

-----
## ⚙️ Configuration

All primary configurations for this project are managed through YAML or Python files located in the `configs/` directory. Please modify these files according to your needs:

  * **`configs/cityscapes.yaml` :** To change the root paths of cityscapes.
  * **`configs/pascal.yaml` :** To change the root paths of pascal.

It's crucial to review and adjust these configurations before running any training or evaluation scripts.

-----

## 📄 License

This project is licensed under the [MIT License]. See the `LICENSE` file for details.

-----

## ✉️ Contact

If you have any questions or suggestions regarding this project, please feel free to contact me via:

  * **Email:** pan.liu@csu.edu.cn

-----