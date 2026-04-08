# GATE PET Model for Voxel-Wise Dosimetry in Radionuclide Therapy

**GATE (Geant4 Application for Tomographic Emission)** is an open-source software developed by the international OpenGATE collaboration for Monte Carlo (MC) simulations in medical physics. Built on top of GEANT4 (GEometry ANd Tracking), it allows realistic modeling of radiation transport and emission tomography systems. It plays a key role in the design and optimization of imaging systems, the development of advanced image processing algorithms, and the implementation of MC dosimetry approaches.

This repository contains the code developed as part of my Master’s thesis, focused on the implementation of a PET scanner model using **GATE** for **personalized voxel-wise dosimetry** of **Yttrium-90 (⁹⁰Y)** in patients undergoing **liver radioembolization (RE)**.

The goal of this project is to support treatment planning optimization and post-treatment verification by allowing **simulation of absorbed dose distributions of patient-specific cases**.

## Workflow 

This project implements a full pipeline for voxel-wise dosimetry in ⁹⁰Y radioembolization, combining MC-GATE simulations, PET image reconstruction, and quantitative absorbed dose analysis. The workflow is structured as follows:

 <img width="4346" height="1993" alt="githubscheme" src="https://github.com/user-attachments/assets/aa954e17-3420-48ca-b533-6e0d5a71adc2" />


## Repository Structure

### Patient-specific Phantom
- **Digital phantom** - Generation of patient-specific phantom in 3D Slicer and conversion for MC-GATE simulations.

### MC-GATE Simulations (GATE 9.2 version)
- **GATE 9.2 Parallel Jobs Tools** - Tools for splitting MC-GATE simulations into multiple smaller jobs and executing them in parallel using Python multiprocessing. This approach reduces computation time by leveraging multiple CPU cores. A merging script combines the resulting ROOT output files into a single dataset.
- **MC-GATE Simulation Files** - Includes simulation macros for:
   - GATE PET scanner model;
   - MC Dosimetry (using ground-truth and simulated PET images);
   - Normalization Simulation.
- **⁹⁰Y Positron Energy Spectrum**  - Input data required for accurate modeling of the ⁹⁰Y radionuclide emission spectrum in PET acquisition simulations.

### Image Reconstruction
- **CASToR Tools** - Graphical user interface (GUI) and utilities for CASToR reconstruction, including conversion from interfile format to NIfTI.  
  *(The code from this study ([GitHub](https://github.com/miguelleaolopes/HiRezBrainPET_git)) was used as a starting point and extended to provide a more user-friendly interface for GATE PET list-mode data processing, with added support for Linux environments.)* 
- **PyTomography Scripts** - Adaptations to PyTomography source files for compatibilty with GATE PET model. Deep Image Prior (DIP) reconstruction and main reconstruction files, including parameter configurations and corresponding reconstruction results.
- **PET Reconstructed Images Analysis/** - Quantitative evaluation and comparison of reconstructed simulated PET images (CASToR vs PyTomography) against ground-truth PET.
- **Activity Quantification** – Conversion of reconstructed PET images from relative count units to activity units.

### MC Dosimetry
- **Dosimetry Calibration Tool** - Calibration of absorbed dose distributions accounting for ⁹⁰Y radioactive decay, administered activity, residual activity and lung shunt factor.
- **MC-GATE Dosimetry Statistical Uncertainty Tool** – Tools for estimating statistical uncertainty (SU) in MC-GATE simulations for each VOI.
- **Dosimetry Analysis** – Computation of mean absorbed doses for each VOI, including dose–volume histograms (DVHs) and dose bar distribution plots. Comparision of MC dosimetry results with the VSV method.

#### Additional Notes
Detailed descriptions of the files are provided in the individual `README.md` files within each folder.

## Contact

Feel free to reach out if you have any questions or suggestions for improvement:

📧 beatrizornelas@tecnico.ulisboa.pt

## Credits
If you find this code useful for your research, please consider citing:

> Ornelas, B. (2026). *Development of a PET GATE model for voxel-wise dosimetry in radionuclide therapy*. Master’s thesis, Instituto Superior Técnico, Universidade de Lisboa, Lisbon, Portugal.
