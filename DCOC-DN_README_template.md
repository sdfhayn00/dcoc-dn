# DCOC-DN: Dual-Constrained Outlier Clustering with DefectNet

## Overview

This repository contains the implementation and datasets for the DCOC-DN framework presented in the paper "Advanced Measurement Analysis for Additive Manufacturing Quality Control: Dual-Constrained Signal Decoupling with Cross-Modal Verification" submitted to *Measurement*.

## Repository Structure

```
dcoc-dn/
├── datasets/
│   ├── 2D_models/           # 2D surface images and corresponding labels
│   │   ├── overflow_case/   # PP material overflow defects
│   │   ├── lack_case/       # PLA material lack defects
│   │   └── piplup_case/     # SLS complex geometry validation
│   ├── 3D_models/
│   │   ├── point_clouds/    # Raw scanned point cloud data (.ply, .pcd)
│   │   ├── reference_models/# CAD reference models (.stl)
│   │   └── defect_annotations/ # Ground truth defect labels
│   ├── labels/
│   │   ├── ground_truth/    # Manual annotation files
│   │   └── annotation_files/# Defect classification labels
│   └── DefectNet/
│       ├── model_weights/   # Pre-trained DefectNet weights
│       └── config_files/    # Network configuration files
├── docs/
│   ├── installation.md     # Setup instructions
│   └── usage_examples.md   # Code examples and tutorials
└── config/
    └── parameter_settings.json # Default DCOC parameters
```

## Dataset Description

### 2D Surface Images
- **Format**: PNG/JPG images (1920×1080 resolution)
- **Content**: Surface texture images captured during 3D scanning
- **Annotation**: Bounding box coordinates for defect regions
- **Cases**: Overflow (PP), Lack (PLA), Piplup (SLS)

### 3D Point Cloud Data
- **Format**: PLY and PCD files
- **Density**: ~50,000-100,000 points per model
- **Precision**: Sub-millimeter accuracy (±0.05mm)
- **Content**: Raw scanned data with XYZ coordinates and normal vectors

### Reference Models
- **Format**: STL triangular mesh files
- **Source**: Original CAD designs used for printing
- **Purpose**: Ground truth for deviation analysis

### Defect Annotations
- **Format**: JSON files with defect cluster information
- **Content**: Centroid positions, volumes, morphology descriptors
- **Validation**: Cross-modal verification results included

## Usage

### Quick Start
```python
import dcoc_dn

# Load dataset
dataset = dcoc_dn.load_dataset('overflow_case')

# Run DCOC analysis
results = dcoc_dn.analyze(
    point_cloud=dataset.point_cloud,
    reference_model=dataset.reference_model,
    surface_image=dataset.surface_image
)

# Visualize results
dcoc_dn.visualize_results(results)
```

### Parameter Configuration
```json
{
    "tau_geo": 0.5,
    "tau_normal": 15.0,
    "dbscan_eps": 2.0,
    "dbscan_min_pts": 10,
    "cross_modal_threshold": 0.8
}
```

## Experimental Results

The datasets support the following key findings reported in the paper:
- **Detection Accuracy**: 96.2% across all test cases
- **False Positive Rate**: 3.8% average
- **Cross-Modal Verification Rate**: 100%
- **Processing Time**: ~180 seconds per analysis

## Citation

If you use this dataset in your research, please cite:

```bibtex
@article{he2024dcoc,
  title={Advanced Measurement Analysis for Additive Manufacturing Quality Control: Dual-Constrained Signal Decoupling with Cross-Modal Verification},
  author={He, Jiajian and Wang, Sisi and Li, Xiping and Sun, Lei and E, Shiju and Zhang, Rui and Kong, Akang and Liao, Qihang},
  journal={Measurement},
  year={2024},
  note={Under Review}
}
```

## License

This dataset is released under the MIT License for academic and research purposes.

## Contact

For questions regarding the dataset or implementation:
- **Corresponding Author**: Xiping Li (xiping.li@zjnu.edu.cn)
- **Primary Contact**: Sisi Wang (sisi.wang@zjnu.edu.cn)

## Acknowledgments

This work was supported by [funding information]. We thank the reviewers for their constructive feedback that improved the quality and reproducibility of this research.
