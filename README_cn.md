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

**PathOmics** 是一个用于 **全视野病理切片（Whole Slide Image, WSI）** 的 **细胞级 → WSI 级放射组学特征提取工具包**。

它支持从 **细胞实例分割结果（GeoJSON）** 出发，计算细胞级特征，并进一步聚合为 **WSI 级特征**，适用于计算病理、数字病理与多模态研究。

## ✨ 功能特性

- 🧬 Cell-level → WSI-level 特征计算流程
- 🧠 支持 first-order、shape 等基础放射组学特征
- 🧩 基于 YAML 的灵活参数配置
- 🏷 支持按细胞类型（cell_type）聚合
- 📦 模块化设计，易于二次开发
- 📝 使用 Python logging，不使用 print
- 🚫 核心 API **不写文件**，完全由用户控制输出

## 📦 安装

### 方法一：通过 PyPI 安装（推荐）

```
pip install pathomics
```

适合 直接使用 / 服务器环境 / 虚拟环境。

> ⚠️ **重要说明（WSI 依赖）**
> **还需手动安装 OpenSlide 系统库**：
>
> ```bash
> # Windows / Linux（conda）
> conda install -c conda-forge openslide openslide-python
> ```

### 方法二：通过 Conda / Mamba 环境（推荐科研环境）

项目提供了完整的环境文件：

```
conda env create -f environment.yaml
conda activate pathomics
```

或使用 mamba（更快）：

```
mamba env create -f environment.yaml
mamba activate pathomics
```

> 该方式特别适合 **WSI / OpenSlide / Linux 服务器** 环境。

## 🚀 快速开始

> 建议先参考 examples/ 文件夹中的示例代码和配置文件

### 示例文件说明

```
examples/
├── example_file.csv        # 批量处理 CSV 示例
├── extract_from_pandas.py  # 批量特征提取示例
└── params.yaml             # 参数配置示例
```

### 1️⃣ 单张 WSI 特征提取（API 方式）

```
from pathomics.extractor import extract

res = extract(
    svs_path="example.svs",
    geojson_path="cells.geojson",
    params_path="params.yaml",
)

wsi_features = res["wsi_features"]
```

### 2️⃣ 批量处理（CSV 驱动，推荐）

CSV 示例（见 examples/example_file.csv）：

```
wsi_path,mask_path
/path/to/wsi_001.svs,/path/to/wsi_001_cells.geojson
/path/to/wsi_002.svs,/path/to/wsi_002_cells.geojson
```

运行示例脚本：

```
python examples/extract_from_pandas.py \
  --input_csv examples/example_file.csv \
  --params examples/params.yaml \
  --out_dir result/
```

输出结果：

```
result/
├── wsi_features.csv
└── run_wsi_feature_extract.log
```

## 📄 许可证

MIT License

## 📬 联系方式

欢迎通过 GitHub Issues 提交问题或建议
