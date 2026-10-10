# DISSECT

DISSECT is a deep semi-supervised learning framework that performs complete deconvolution of gene expression mixtures such as bulk RNAseq, proteomics and spatial transcriptomics. The manuscript is available at [Genome Biology](https://link.springer.com/article/10.1186/s13059-024-03251-5).

This repository contains the functions to run DISSECT interactively in Python. The code to reproduce figures and run deconvolution pipeline through comamnd line is available [here](https://github.com/imsb-uke/deconvolution).  

## macOS compatibility

This local checkout includes a macOS-compatible dependency set in
`requirements.txt`. It uses `tensorflow==2.20.0` instead of the unavailable
macOS package `tensorflow-gpu==2.7.0`, and `tf-keras==2.20.1` to retain the
legacy `tf.keras` API used by DISSECT. This configuration uses TensorFlow on
CPU; it does not enable CUDA GPU acceleration.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. Folder tutorials include notebooks to get started.

## Prerequisites

conda >= v22 through [Anaconda](https://docs.anaconda.com/free/anaconda/install/index.html) or [miniconda](https://docs.conda.io/projects/miniconda/en/latest/miniconda-install.html).

## Installing
```shell
## Installation

# Create and activate virtual environment. This is recommended to avoid conflict in dependencies.
conda create -y -n dissect python=3.9
conda activate dissect

# Clone DISSECT
git clone https://github.com/imsb-uke/DISSECT

# Install dependencies and DISSECT

pip install -r DISSECT/requirements.txt --use-deprecated=legacy-resolver
pip install DISSECT/.

# Install jupyter lab for interactive execution of notebooks
conda install -y jupyter

## Tutorials to get started
# Go to tutorials directory within DISSECT
cd DISSECT/tutorials

## Launch jupyter lab
jupyter notebook

```
## GPU usage on Linux

The upstream DISSECT setup supports CUDA on Linux with a compatible NVIDIA
driver and CUDA/cuDNN installation. The macOS-compatible requirements above
use CPU TensorFlow instead. On a CUDA-enabled Linux system, check the devices
available to TensorFlow with:

```python
import tensorflow as tf
gpus = tf.config.list_physical_devices("GPU")
print(gpus)

```
This will output a list of the available GPU devices as the output below where we have 1 GPU available. 
```
[PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')] 
```
In case there are multiple GPUs available, a particular GPU can be set by,

```python
gpu_number = 0 # Using only the first GPU
tf.config.experimental.set_visible_devices(gpus[gpu_number], 'GPU')
```

## Tutorials
Interactive tutorials including required data are available as part of this repository at [Tutorials](https://github.com/imsb-uke/DISSECT/tree/main/tutorials).
1. [tutorial.ipynb](https://github.com/imsb-uke/DISSECT/tree/main/tutorials/tutorial.ipynb): Step by step deconvolution for bulk
2. [tutorial_spatial.ipynb](https://github.com/imsb-uke/DISSECT/tree/main/tutorials/tutorial_spatial.ipynb): Step by step deconvolution of spatial transcriptomics data (10x Visium)

### A note on the supported formats
bulk RNAseq/Proteomics: A tab seperated file (gene symbols in rows, sample names in columns), or an h5ad compatible with Scanpy >=1.8.0.

scRNAseq: An h5ad compatible with Scanpy >=1.8.0. The cell metadata (.obs) must contain cell type labels (By default in column cell_type)

Spatial transcriptomics: A h5ad compatible with Scanpy >=1.8.0.

Gene ID formats should match between scRNAseq and bulk/spatial data but can be anything (HGNC symbols, ENSEMBL etc.).

The code is also available via [Zenodo](https://zenodo.org/doi/10.5281/zenodo.10570403)

To get answers quickly for a problem or feature request, please open an [issue](https://github.com/imsb-uke/DISSECT/issues).

## References
[1] Khatri, R., Machart, P. & Bonn, S. DISSECT: deep semi-supervised consistency regularization for accurate cell type fraction and gene expression estimation. Genome Biol 25, 112 (2024). https://doi.org/10.1186/s13059-024-03251-5
