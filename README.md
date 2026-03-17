
```markdown
# Automated Flood Mapping Using Sentinel-2A Imagery and Machine Learning

![Project Status](https://img.shields.io/badge/status-completed-brightgreen)
![Python](https://img.shields.io/badge/python-3.8%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)

## 📋 Overview

This research project develops an automated flood mapping framework using Sentinel-2A satellite imagery and supervised machine learning classification models. The study focuses on Nairobi, Kenya, addressing the critical need for rapid and accurate flood assessment tools to support disaster response and urban planning.

**Key Achievement**: Random Forest with Bagging achieved **91.6% accuracy** in flood detection, identifying widespread inundation affecting over 110 buildings in the study area.

## 🎯 Problem Statement

- Traditional flood assessment in Nairobi relies on slow, manual methods with limited spatial detail
- Sentinel-2 imagery provides detailed observations but requires complex pre-processing
- Need for automated ML approaches to transform satellite data into accurate flood maps for rapid decision-making

## 🚀 Features

- **Automated Data Processing**: Downloads and pre-processes Sentinel-2 Level-2A imagery
- **Spectral Indices Calculation**: Computes multiple water-sensitive indices
- **Multiple ML Models**: Implements and compares 8 different classification algorithms
- **Flood Extent Mapping**: Generates pixel-wise flood classification maps
- **Post-Processing**: Applies morphological operations for enhanced map quality
- **Impact Assessment**: Estimates flooded areas and affected infrastructure

## 🗺️ Study Area

- **Location**: Nairobi, Kenya
- **Satellite Data**: Sentinel-2A (ESA Copernicus Program)
- **Spatial Resolution**: 10m (resampled from 10-60m bands)
- **Temporal Coverage**: Focus on recent flood events

## 📊 Machine Learning Models Evaluated

| Model | Accuracy (%) |
|-------|-------------|
| Random Forest with Bagging | 91.6 |
| Gradient Boosting | 91.1 |
| AdaBoost with Decision Tree | 91.0 |
| Random Forest | 90.9 |
| XGBOOST | 90.6 |
| CNN 1D | 89.6 |
| Support Vector Machine (LSVM) | 86.1 |
| K-Nearest Neighbors (KNN) | 84.0 |

## 🛠️ Methodology

### 1. Data Acquisition
- Download Sentinel-2 Level-2A (Bottom of Atmosphere) imagery from Copernicus Open Access Hub
- 13 spectral bands covering visible to shortwave infrared

### 2. Pre-processing
- Resample all bands to 10m resolution
- Create 3D image stack (bands × height × width)
- Band-by-band normalization

### 3. Feature Engineering
Key spectral indices calculated:

```
MNDWI = (B03 - B11) / (B03 + B11)      # Modified Normalized Difference Water Index
NDVI = (B08 - B04) / (B08 + B04)        # Normalized Difference Vegetation Index
NDFI = (B04 - B12) / (B04 + B12)        # Normalized Difference Flood Index
```

### 4. Training Data Construction
- Polygon-based labeling in QGIS
- Pixel extraction for flooded (1) and non-flooded (0) areas
- Train-test split for supervised learning

### 5. Model Training & Evaluation
- Implement multiple classification algorithms
- Cross-validation and accuracy assessment
- Confusion matrix analysis

### 6. Flood Map Generation
- Apply best model to full image stack
- Post-processing with morphological operators
- Area calculation and validation
# Install dependencies
pip install -r requirements.txt
```

## 📋 Requirements

```
numpy>=1.21.0
pandas>=1.3.0
scikit-learn>=1.0.0
xgboost>=1.5.0
tensorflow>=2.8.0
rasterio>=1.2.0
geopandas>=0.10.0
sentinelhub>=3.7.0
matplotlib>=3.4.0
seaborn>=0.11.0
opencv-python>=4.5.0
```

## 💻 Usage

### 1. Download Sentinel-2 Data
```python
from src.data_download import download_sentinel2

# Download imagery for specific tile and date
download_sentinel2(tile="your_tile_id", date="2024-01-01", output_dir="./data")
```

### 2. Pre-process Images
```python
from src.preprocessing import preprocess_image

# Resample bands and create image stack
image_stack = preprocess_image("./data/raw", "./data/processed")
```

### 3. Calculate Spectral Indices
```python
from src.features import calculate_indices

# Generate water-sensitive indices
indices = calculate_indices(image_stack)
```

### 4. Train Models
```python
from src.models import train_all_models

# Train and evaluate all classifiers
results = train_all_models(training_data, labels)
print(results)
```

### 5. Generate Flood Map
```python
from src.mapping import create_flood_map

# Create final flood extent map
flood_map = create_flood_map(best_model, processed_image)
```

## 📁 Repository Structure

```
flood-mapping-sentinel2-ml/
│
├── data/
│   ├── raw/                # Original Sentinel-2 images
│   ├── processed/          # Pre-processed image stacks
│   ├── training/           # Training polygons and labels
│   └── results/            # Output maps and metrics
│
├── src/
│   ├── data_download.py    # Copernicus data acquisition
│   ├── preprocessing.py    # Band resampling and normalization
│   ├── features.py         # Spectral indices calculation
│   ├── models.py           # ML model implementations
│   ├── evaluation.py       # Accuracy assessment
│   └── mapping.py          # Flood map generation
│
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_feature_engineering.ipynb
│   └── 03_model_comparison.ipynb
│
├── tests/                  # Unit tests
├── docs/                    # Documentation
├── requirements.txt         # Dependencies
├── README.md                # This file
└── LICENSE                  # MIT License
```

## 📈 Results

### Best Model Performance
- **Algorithm**: Random Forest with Bagging
- **Accuracy**: 91.6%
- **Key Features**: MNDWI, NDFI, and SWIR bands most important for flood detection

### Flood Impact Assessment
- Identified **110+ buildings** within flooded areas
- Flood extent maps validated against government records
- Spatial distribution maps available in `/results`

## 🔮 Future Directions

1. **Temporal Analysis**: Extend study to 2015-2025 for long-term trend evaluation
2. **Advanced Models**: Incorporate deep learning architectures (CNNs, Transformers)
3. **Geographic Expansion**: Cover entire Nairobi City for comprehensive assessment
4. **Hydrological Integration**: Combine with watershed and drainage system analysis
5. **Predictive Tools**: Develop early warning systems for flood forecasting

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📚 Citation

If you use this code in your research, please cite:

```bibtex
@article{antwi2026automated,
  title={Automated Flood Mapping Using Sentinel-2A Imagery and Machine Learning Classification Models},
  author={Antwi, Pascal and Ugutu, George and Ochingo, Joab Jared and Evance, Ouma},
  year={2026}
}
```


- **ESA Copernicus Program** for providing free Sentinel-2 imagery
- **Strathmore University** for research support
- **University of Nairobi** and **Egerton University** for collaboration
- **Technical University of Kenya** for technical guidance

```

This README provides:
- Clear project overview and objectives
- Technical methodology explanation
- Installation and usage instructions
- Repository structure
- Results and impact assessment
- Future directions
- Proper attribution and citation information

You can customize the contact information, GitHub username, and any specific implementation details based on your actual code.
