# Brain-Tumor-Segmentation-with-U-NET

This repository contains a comparative study of **2D and 3D U-Net** architectures for the automated segmentation of brain tumors using the **BraTS 2020** dataset. The project benchmarks slice-level precision against volumetric spatial consistency, providing a foundation for clinical biomarker extraction and **Digital Twin** applications in personalized medicine.



## 📊 Performance Benchmark
The following results were achieved on the validation set using a hybrid loss function (Dice Loss + Binary Cross-Entropy).

| Model Architecture | Dice Coefficient | Validation Loss | Observation |
| :--- | :--- | :--- | :--- |
| **2D U-Net** | **0.9394** | **0.0356** | High-precision axial slice segmentation. |
| **Standard 3D U-Net** | 0.7584 | 0.1363 | Base volumetric context. |
| **Improved Residual 3D U-Net** | **0.7974** | **0.1213** | **Residual blocks** + **Mixed Precision**. |



---

##  Key Technical Features

### 1. Volumetric Data Engineering
* **Multi-modal MRI Processing:** Integration of FLAIR, T1, T2, and T1ce sequences.
* **3D Data Generator:** Custom `tf.keras.utils.Sequence` implementation for memory-efficient training.
* **Smart Cropping:** Automated extraction of $64 \times 128 \times 128$ sub-volumes focusing on the tumor core to optimize GPU VRAM.

### 2. Advanced Neural Architectures
* **Improved 3D U-Net:** Features **Residual Blocks** to improve gradient flow and **Batch Normalization** for training stability.
* **Mixed Precision Training:** Utilized `mixed_float16` policies to accelerate 3D convolutional operations on Colab GPUs.
* **Hybrid Loss:** Optimized training using a weighted combination of **Dice Loss** and **Binary Cross-Entropy**.

### 3. Clinical Metrics (Volumetry)
Beyond segmentation masks, the pipeline translates AI predictions into physical biomarkers:
* **Voxel-to-ml Conversion:** Extracts `pixdim` metadata from NIfTI headers.
* **Anatomical Consistency:** Validates tumor structure across **Axial**, **Coronal**, and **Sagittal** planes to ensure realistic 3D connectivity.



---

##  How to Run

### 1. Installation
```bash
git clone [https://github.com/alirahme17/brats-2d-3d-unet-benchmark.git](https://github.com/alirahme17/brats-2d-3d-unet-benchmark.git)
cd brats-2d-3d-unet-benchmark
pip install -r requirements.txt
```


### 2. Dataset Structure
Ensure your BraTS 2020 data is organized as follows:
/data/
  /BraTS20_Training_001/
    BraTS20_Training_001_flair.nii
    BraTS20_Training_001_seg.nii


### 3. Usage
* Training: Run the 2D and 3D training notebooks to generate weights.
* Evaluation: Use the Volumetric_Analysis module to compare ml measurements across models.

## The "Volume-Dice Paradox"
One of the key findings of this study is that while the 2D Model achieved a higher Dice score, the 3D Model consistently identified larger, more connected tumor volumes. This suggests that 3D architectures are superior for monitoring longitudinal growth, whereas 2D models are optimal for high-precision contouring.

## About the Author

**Ali Rahme** 

* M.Sc. Student in Image and Signal Processing | École Centrale de Nantes 
* B.Sc. in Computer and Communication Engineering | Lebanese University 
* Specialization: AI, Deep Learning, Computer Vision, and Computational Methods for Medical Imaging.
