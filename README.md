# SpatialMETA

spatialMETA is an excellent method for integrating spatial multi-omics data. SMOI aligns ST and SM to a unified resolution, integrates single or multiple sample data to identify cross-modal spatial patterns, and offers extensive visualization and analysis functions. The original project provides a valuable framework for spatial multiomics research, and this forked version optimizes the installation process to resolve compatibility issues encountered in the official configuration.
<img src="./docs/source/_static/imgs/spatialmeta_2025.png" />
## Documentation
[Official Documentation](https://spatialmeta.readthedocs.io/en/latest/)

## Important Notes (Compatibility Optimization)
The original installation configuration (including `requirements.txt`, `setup.py`, and `environment.yml`) may lead to installation failures due to dependency version incompatibility, non-standard package naming, and unstable third-party dependency sources. This forked version optimizes the installation process to ensure smooth deployment, with core issues and modifications as follows:
- **Version incompatibility**: The original `scikit-learn==1.5.0`/`torch==2.2.2+cu121` are incompatible with the project; downgraded to stable, compatible versions.
- **Non-standard package names**: Fixed incorrect package naming (e.g., `pyimzml` → `pyimzML`, `python_dotplot` → `python-dotplot`) that caused installation failures.
- **Unstable dependency sources**: Removed reliance on non-official third-party sources (e.g., `miropsota.github.io`) to use standard PyPI/NVIDIA sources.

## Installation
Recommended to use Python 3.9 environment (consistent with the original recommendation, optimized for dependency compatibility).

### Step 1: Create a new conda environment (Recommended)
```shell
# Create a clean environment to avoid dependency conflicts
conda create -n spatialmeta python=3.9 -y
conda activate spatialmeta

# Upgrade pip to the latest version
pip install --upgrade pip
```

### Step 2: Install via optimized source (Forked Version)
```shell
# Clone the optimized forked repository (包含修正后的 requirements.txt)
# 方式1: SSH 地址（推荐，需配置 GitHub SSH 密钥）
git clone git@github.com:nkfff/SpatialMETA.git
# 方式2: HTTPS 地址（无需密钥，适合快速克隆）
# git clone https://github.com/nkfff/SpatialMETA.git

cd SpatialMETA

# Install compatible dependencies (core modification: fixed version and package name)
pip install -r requirements.txt

# Install spatialMETA
python setup.py install
```

### Alternative: Install via PyPI (Compatible Version)
If source installation fails, use the verified compatible PyPI version:
```shell
pip install spatialmeta==0.0.3.0
```

### Key Modifications to Installation Configuration
Compared with the original project, the following critical adjustments are made in this version:
1. **Core dependency version adjustment**:
   - `scikit-learn`: Downgraded from 1.5.0 (original) to 0.24.1 (compatible with the project's core logic)
   - `PyTorch/torchvision`: Downgraded from 2.2.2+cu121/0.17.2 to 1.13.1/0.14.1 (resolved CUDA/API compatibility issues)
   - `setuptools`: Updated from 59.5.0 to 80.9.0 (resolved `pkg_resources` deprecation warnings)
2. **Package name standardization**:
   - `pyimzml` → `pyimzML` (matches PyPI official package name)
   - `python_dotplot` → `python-dotplot` (fixed underscore/hyphen naming error)
3. **Dependency source optimization**:
   - Removed unstable third-party sources (e.g., `https://miropsota.github.io/torch_packages_builder`)
   - Use standard PyPI/NVIDIA sources for more reliable installation
4. **Simplified environment configuration**:
   - Removed unused dependencies (e.g., commented-out `pytorch3d`, `scikit-image`) to reduce installation complexity

## Verify Installation
To confirm successful installation and compatibility:
```shell
python -c "
import spatialmeta
import torch
import scanpy
print('✅ spatialMETA installed successfully!')
print(f'🔧 PyTorch version: {torch.__version__} (expected: 1.13.1)')
print(f'🔧 scikit-learn version: {__import__('sklearn').__version__} (expected: 0.24.1)')
"
```

## Change Log
### Forked Version Modifications
- Optimized `requirements.txt` (core change): Fixed dependency versions and package naming to resolve installation failures
- Simplified dependency sources and installation steps for better stability
- Added installation verification commands

### Original Project Changelog
- 0.0.2 (2025-03-06)
  - Update `spatialmeta.model.AlignmentModule` 
  - Update `spatialmeta.model.ConditionalVAESTSM`
```
