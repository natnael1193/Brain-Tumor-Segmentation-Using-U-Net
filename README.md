# Brain Tumor Segmentation Using U-Net

A deep learning project for brain tumor segmentation using the U-Net architecture on the BRISC 2025 dataset.

## Project Overview

This project implements a U-Net convolutional neural network for semantic segmentation of brain tumors from MRI scans. The implementation includes:

- **U-Net Architecture**: Encoder-decoder structure with skip connections
- **Custom Loss Function**: Combination of binary cross-entropy and Dice loss
- **Data Preprocessing**: Image loading, resizing, and normalization
- **Model Training**: Multiple training iterations with improvements
- **Visualization**: Side-by-side comparison of original images, ground truth masks, and predictions

## Dataset

This project uses the **BRISC 2025** (BRain tumor Image Segmentation & Classification) dataset:

- **6,000 T1-weighted MRI slices** (5,000 train / 1,000 test)
- **Four classes**: Glioma, Meningioma, Pituitary Tumor, No Tumor
- **Pixel-wise segmentation masks** reviewed by radiologists
- **Three anatomical planes**: Axial, Coronal, Sagittal

### Dataset Structure
```
data/
├── segmentation_task/
│   ├── train/
│   │   ├── images/     # MRI scans (.jpg)
│   │   └── masks/      # Segmentation masks (.png)
│   └── test/
│       ├── images/
│       └── masks/
└── classification_task/
    ├── glioma/
    ├── meningioma/
    ├── pituitary/
    └── no_tumor/
```

## Requirements

```bash
pip install tensorflow opencv-python numpy matplotlib
```

## Project Structure

- `index.ipynb` - Main Jupyter notebook containing the complete implementation
- `data/` - Dataset directory containing BRISC 2025 data
- `model/` - Directory for saving trained models
- `README.md` - This file

## Implementation Details

### U-Net Architecture
- **Input**: 128×128×3 RGB images
- **Encoder**: Two downsampling blocks with Conv2D layers
- **Bottleneck**: Feature extraction at reduced spatial resolution
- **Decoder**: Two upsampling blocks with skip connections
- **Output**: Binary segmentation mask (sigmoid activation)

### Loss Function
The model uses a combined loss function:
```python
loss = 0.5 * binary_crossentropy + dice_loss
```

### Training Improvements
1. **Version 1**: Basic U-Net with 20 epochs
2. **Version 2**: Improved loss weighting with 40 epochs
3. **Version 3**: Enhanced architecture with BatchNormalization

### Key Features
- **Image Preprocessing**: Resizing to 128×128, normalization to [0,1]
- **Mask Processing**: Binary conversion and channel expansion
- **Data Loading**: Automated pairing of images and masks
- **Model Saving**: H5 format for easy deployment

## Usage

1. **Setup Environment**:
   ```bash
   pip install tensorflow opencv-python numpy matplotlib
   ```

2. **Run the Notebook**:
   - Open `index.ipynb` in Jupyter
   - Execute cells sequentially
   - Models will be saved to `./model/` directory

3. **Training**:
   - Load training data from `./data/segmentation_task/train/`
   - Train the U-Net model with custom loss
   - Monitor training progress and metrics

4. **Inference**:
   - Load trained model from saved H5 files
   - Perform predictions on test images
   - Visualize results with matplotlib

## Model Performance

The project includes iterative improvements:
- **Model V1**: Basic U-Net (20 epochs)
- **Model V2**: Improved loss weighting (40 epochs)  
- **Model V3**: Enhanced with BatchNormalization

## File Naming Convention

Images follow the BRISC pattern:
```
brisc2025_<split>_<index>_<tumor>_<view>_<sequence>.jpg
```

Example: `brisc2025_train_00001_gl_ax_t1.jpg`

## Citation

If you use this project or the BRISC dataset, please cite:

```bibtex
@article{fateh2025brisc,
  title={Brisc: Annotated dataset for brain tumor segmentation and classification with swin-hafnet},
  author={Fateh, Amirreza and Rezvani, Yasin and Moayedi, Sara and Rezvani, Sadjad and Fateh, Fatemeh and Fateh, Mansoor and Abolghasemi, Vahid},
  journal={arXiv preprint arXiv:2506.14318},
  year={2025}
}
```

## Course Information

**Project for**: Digital Signal and Image Processing  
**University**: Università degli Studi di Milano-Bicocca  
**Academic Year**: 2024-2025
