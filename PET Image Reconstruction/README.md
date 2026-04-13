## PET Image Reconstruction

The list-mode ROOT file generated from the GATE PET model was reconstructed into PET images using two external software packages: CASToR and PyTomography.

### CASToR Tools

**Graphical user interface (GUI) tools** developed to simplify the use of CASToR utilities and streamline the PET reconstruction workflow. These tools provide a more user-friendly alternative to command-line execution, particularly for handling GATE output data.

**The following code was developed:**

- **[castorGATERootToCastor_tool_GUI.py](./CASToR%20Tools/castorGATERootToCastor_tool_GUI.py)** – GUI application for converting GATE list-mode ROOT output files into CASToR format data files (`.cdh`) for PET, SPECT, or CT reconstruction. It provides an intuitive interface for the `castor-GATERootToCastor` tool.

- **[castor-recon_tool_GUI.py](./CASToR%20Tools/castor-recon_tool_GUI.py)** – GUI application for configuring and running image reconstruction workflows using CASToR. It simplifies interaction with the main reconstruction tool, `castor-recon`, for PET, SPECT, and CT modalities.

**Notes:**
- Additional information about each tool is available through the **“About”** section within the GUI.  
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

### PET Reconstructed Images Analysis

### Activity Quantification
