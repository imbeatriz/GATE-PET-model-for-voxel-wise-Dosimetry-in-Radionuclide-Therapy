# GATE PET Model for Voxel-Wise Dosimetry in Radionuclide Therapy

**GATE (Geant4 Application for Tomographic Emission)** is an open-source software developed by the international OpenGATE collaboration for Monte Carlo (MC) simulations in medical physics. Built on top of GEANT4 (GEometry ANd Tracking), it allows realistic modeling of radiation transport and emission tomography systems. It plays a key role in the design and optimization of imaging systems, the development of advanced image processing algorithms, and the implementation of MC dosimetry approaches.

This repository contains the code developed as part of my Master’s thesis, focused on the implementation of a PET scanner model using **GATE** for **personalized voxel-wise dosimetry** of **Yttrium-90 (⁹⁰Y)** in patients undergoing **liver radioembolization (RE)**.

The goal of this work is to support treatment planning optimization and post-treatment verification by allowing **simulation of absorbed dose distributions of patient-specific cases**.

## Contact

Feel free to reach out if you have any questions or suggestions:

📧 beatrizornelas@tecnico.ulisboa.pt

## Repository Structure

### Digital Phantom
- Digital phantom generation and processing files

### GATE
- GATE 9.2 simulation files  
- Parallel job execution tools  
- MC-GATE simulation setup  
- ⁹⁰Y positron energy spectrum  

### Image Reconstruction
- CASToR tools and configurations  
- PyTomography scripts  
- Reconstruction analysis results  

### MC Dosimetry
- Dosimetry calibration tools  
- Statistical uncertainty analysis  
- Absorbed dose analysis workflows  

## Workflow 

The dosimetry worflow is as follows: 

## Credits
If you find this code useful, please consider citing:

> Ornelas, B. (2026). *Development of a PET GATE model for voxel-wise dosimetry in radionuclide therapy*. Master’s thesis, Instituto Superior Técnico, Universidade de Lisboa, Lisbon, Portugal.
