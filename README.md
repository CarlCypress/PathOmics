# PathOmics

<p align="center">
  <a href="README.md">English</a> |
  <a href="README_cn.md">中文</a>
</p>

<p align="center">
  <img src="https://img.shields.io/pypi/v/pathomics.svg" />
  <img src="https://img.shields.io/pypi/pyversions/pathomics.svg" />
  <img src="https://img.shields.io/badge/License-MIT-blue" />
  <img src="https://img.shields.io/badge/Domain-Computational%20Pathology-brightgreen" />
</p>

**PathOmics** is a **cell-level → WSI-level radiomics feature extraction toolkit** for **Whole Slide Images (WSI)**.

It supports starting from **cell instance segmentation results (GeoJSON)** to compute cell-level features and further aggregate them into **WSI-level features**, making it suitable for computational pathology, digital pathology, and multimodal research.

## ✨ Features

- 🧬 Cell-level → WSI-level feature computation pipeline  
- 🧠 Supports basic radiomics features such as first-order and shape  
- 🧩 Flexible YAML-based parameter configuration  
- 🏷 Supports aggregation by cell type (`cell_type`)  
- 📦 Modular design, easy to extend and customize  
- 📝 Uses Python logging, no `print` statements  
- 🚫 Core APIs **do not write files**, output is fully controlled by the user  

## 📦 Installation

### Method 1: Install via PyPI (Recommended)
```
pip install pathomics
```
Suitable for direct usage, server environments, and virtual environments.

> ⚠️ **Important notice (WSI dependency)**  
> **The OpenSlide system library must be installed manually**:
>
> ```bash
> # Windows / Linux (conda)
> conda install -c conda-forge openslide openslide-python
> ```

### Method 2: Install via Conda / Mamba Environment (Recommended for research)

The project provides a complete environment file:
```
conda env create -f environment.yaml
conda activate pathomics
```
Or using mamba (faster):
```
mamba env create -f environment.yaml
mamba activate pathomics
```
> This method is especially suitable for **WSI / OpenSlide / Linux server** environments.

## 🚀 Quick Start

> It is recommended to first refer to the example code and configuration files in the `examples/` directory.

### Example files overview
```
examples/
├── example_file.csv    # CSV example for batch processing
├── extract_from_pandas.py # Batch feature extraction example
└── params.yaml       # Parameter configuration example
```
### 1️⃣ Single WSI feature extraction (API usage)
```
from pathomics.extractor import extract

res = extract(
    svs_path="example.svs",
    geojson_path="cells.geojson",
    params_path="params.yaml",
)

wsi_features = res["wsi_features"]
```
### 2️⃣ Batch processing (CSV-driven, recommended)

CSV example (see `examples/example_file.csv`):
```
wsi_path,mask_path
/path/to/wsi_001.svs,/path/to/wsi_001_cells.geojson
/path/to/wsi_002.svs,/path/to/wsi_002_cells.geojson
```
Run the example script:
```
python examples/extract_from_pandas.py \
  --input_csv examples/example_file.csv \
  --params examples/params.yaml \
  --out_dir result/
```
Output results:
```
result/
├── wsi_features.csv
└── run_wsi_feature_extract.log
```
## 📄 License

MIT License

## 📬 Contact

Feel free to submit issues or suggestions via GitHub Issues
