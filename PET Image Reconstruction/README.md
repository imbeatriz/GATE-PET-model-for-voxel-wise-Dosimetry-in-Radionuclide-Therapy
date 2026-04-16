## PET Image Reconstruction

The list-mode ROOT file generated from the GATE PET model was reconstructed into PET images using two external software packages: CASToR and PyTomography.

### CASToR Tools

**Graphical user interface (GUI) tools** developed to simplify the use of CASToR utilities and streamline the PET reconstruction workflow. These tools provide a more user-friendly alternative to command-line execution, particularly for handling GATE output data.

**The following code was developed:**

- **[castorGATERootToCastor_tool_GUI.py](./CASToR%20Tools/castorGATERootToCastor_tool_GUI.py)** – GUI application for converting GATE list-mode ROOT output files into CASToR format data files (`.cdh`) for PET, SPECT, or CT reconstruction. It provides an intuitive interface for the `castor-GATERootToCastor` tool.

- **[castor-recon_tool_GUI.py](./CASToR%20Tools/castor-recon_tool_GUI.py)** – GUI application for configuring and running image reconstruction workflows using CASToR. It simplifies interaction with the main reconstruction tool, `castor-recon`, for PET, SPECT, and CT modalities.

⚠️**Notes:**
- Additional information about each tool is available through the `About` section.  
- For detailed command-line options, run the corresponding CASToR tool directly in the terminal (e.g., `castor-recon` or `castor-GATERootToCastor`).

<p align="center">
  <img src="https://github.com/user-attachments/assets/25fff246-fa67-4e4d-86c6-f35ecea7862d" width="48%" />
  <img src="https://github.com/user-attachments/assets/f7c0ff99-adac-49f6-95c2-bf4f130febdb" width="48%" />
</p>

<p align="center">
  <em>Figure 1 – castor-GATERootToCastor GUI &nbsp;&nbsp;&nbsp;&nbsp; Figure 2 – castor-recon GUI </em>
</p>

- **[CASToR_Interfile_to_Nifti_converter_tool.py](./CASToR%20Tools/CASToR_Interfile_to_Nifti_converter_tool.py)** – This script converts images reconstructed with CASToR from Interfile (.hdr/.img) format to NIfTI (.nii) format.

<p align="center">
  <img src="https://github.com/user-attachments/assets/deffc0e8-4c6b-4402-a991-a1107fbb6dd9" width="700" />
</p>

<p align="center">
  <em>Figure 1 – CASToR Interfile to NIfTI conversion tool</em>
</p>

- **[AlignCASToR_reconstructions.ipynb](./CASToR%20Tools/AlignCASToR_reconstructions.ipynb)** – This script aligns CASToR reconstructed PET images with segmentation masks, ensuring spatial consistency with the VOIs in analysis and CT image.

### PyTomography Scripts

This folder contains adaptations of PyTomography source (`.py`) files to ensure compatibility with the GATE PET model. It includes the full reconstruction workflow, incorporating Deep Image Prior (DIP) reconstruction, main reconstruction scripts, parameter configurations, and the corresponding reconstruction results.

⚠️ **Note: To run PyTomography with the developed GATE PET model, replace the original `sss.py` and `shared.py` files with the modified versions provided in the *PET Image Reconstruction/PyTomography Scripts* folder.**

**The following code was developed:**

- **[shared.py](./PyTomography%20Scripts/shared.py)** – Contains functions related to **random coincidence correction**.  
  The functions `sinogram_coordinates` and `sinogram_to_spatial` were adapted to match the PET scanner geometry used in this work. Additionally, `listmode_to_sinogram`, which converts PET list-mode data into sinograms for randoms correction, was modified for the Philips Vereos system.

- **[sss.py](./PyTomography%20Scripts/sss.py)** – Implements **scatter coincidence correction** using the Single Scatter Simulation (SSS) algorithm.  
  The `scale_estimated_scatter` function was adapted for compatibility with the Philips Vereos PET scanner geometry.

- **[DIP_reconstruction_Y90.ipynb](./PyTomography%20Scripts/DIP_reconstruction_Y90.ipynb)** – Notebook implementing the **DIP** reconstruction method.  
  DIP is an unsupervised technique that leverages anatomical images (CT or MRI) as prior information to improve PET image quality. Unlike conventional deep learning approaches, it does not require large training datasets, instead learning structural information directly from the patient data.  

In this work, DIP is used to denoise low-quality PET images and improve signal-to-noise ratio (SNR), guided by anatomical information. The implementation follows the approach described by [Gong et al.](https://ieeexplore.ieee.org/document/8581448)

<p align="center">
  <img src="https://github.com/user-attachments/assets/9490a395-6f9a-4b8a-b46a-d5a5acb19af5" width="700" />
</p>

<p align="center">
  <em>Figure 1 – 3D U-Net architecture used for DIP reconstruction</em>
</p>

⚠️**Notes:**
 - Additional details on the DIP framework and parameter settings can be found in the master’s thesis document.

- **[PyTomography_reconstruction.ipynb](./PyTomography%20Scripts/PyTomography_reconstruction.ipynb)** – Main reconstruction notebook containing the workflow used in this project, including parameter configuration and reconstruction steps.

### PET Reconstructed Images Analysis

Quantitative evaluation and comparison of reconstructed simulated PET images from both reconstruction frameworks (**CASToR** and **PyTomography**) against the ground-truth PET image.

To assess image quality and quantitative performance, several evaluation metrics were used, including Signal-to-Noise Ratio (SNR), Contrast-to-Noise Ratio (CNR), Tumour-to-Background Ratio (TBR), Contrast Recovery Coefficient (CRC), Root Mean Square Error (RMSE), Structural Similarity Index Measure (SSIM), Peak Signal-to-Noise Ratio (PSNR), and Concordance Correlation Coefficient (CCC).

**The following code was developed:** 

- **[CASToR_PET_reconstruction_Analysis.ipynb](./PET%20Reconstructed%20Images%20Analysis/CASToR_PET_reconstruction_Analysis.ipynb)** – Notebook containing the evaluation of multiple reconstruction settings in CASToR, leading to the selection of the final configuration used for GATE simulated PET images.

- **[CASToR_vs_PyTomography_Reconstructions_Analysis.ipynb](./PET%20Reconstructed%20Images%20Analysis/CASToR_vs_PyTomography_Reconstructions_Analysis.ipynb)** – Notebook presenting the analysis of PyTomography reconstruction settings and a quantitative comparison between the final reconstructed PET images from CASToR and PyTomography against the ground-truth PET image.

### Activity Quantification

This folder contains the conversion of the final reconstructed PET image (obtained with CASToR) from relative count units to absolute activity units, allowing quantitative analysis for RE.

**The following code was developed:**

- **[CASToR_PET_reconstructed_Calibration.ipynb](./Activity%20Quantification/CASToR_PET_reconstructed_Calibration.ipynb)** – Thus script calibrates CASToR reconstructed PET images using system-specific calibration factors, including the sensitivity of the Philips Vereos scanner (cps/MBq) and the rescale slope.

