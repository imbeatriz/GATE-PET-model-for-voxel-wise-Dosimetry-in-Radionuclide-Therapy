# GATE PET Model for Voxel-Wise Dosimetry in Radionuclide Therapy

**GATE (Geant4 Application for Tomographic Emission)** is an open-source software developed by the international OpenGATE collaboration for Monte Carlo (MC) simulations in medical physics. Built on top of GEANT4 (GEometry ANd Tracking), it allows realistic modeling of radiation transport and emission tomography systems. It plays a key role in the design and optimization of imaging systems, the development of advanced image processing algorithms, and the implementation of MC dosimetry approaches.

This repository contains the code developed as part of my Master’s thesis, focused on the implementation of a PET scanner model using **GATE** for **personalized voxel-wise dosimetry** of **Yttrium-90 (⁹⁰Y)** in patients undergoing **liver radioembolization (RE)**.

The goal of this work is to support treatment planning optimization and post-treatment verification by allowing **simulation of absorbed dose distributions of patient-specific cases**.

## Project Overview

This project implements a full pipeline for voxel-wise dosimetry in ⁹⁰Y radioembolization, combining MC simulations with PET image reconstruction and quantitative dose analysis.

## Contact

Feel free to reach out if you have any questions or suggestions:

📧 beatrizornelas@tecnico.ulisboa.pt

## Workflow 

The dosimetry pipeline is as follows: 

Patient-specific Phantom → GATE Simulation → PET Reconstruction → Activity quantification → MC Dosimetry

## Repository Structure

### Patient-specific Phantom
- Digital phantom - generation and processing files on 3D Slicer for GATE simulation

### GATE 9.2
- Parallel job execution Tools - splitting a GATE simulation into multiple smaller jobs and runs them in parallel using Python's multiprocessing
- MC-GATE simulation files - includes MC dosimetry simulation files and GATE PET model simulation of PET acquisition
- ⁹⁰Y positron energy spectrum  - includes the files necessary for the GATE PET model for the PET acquisition for the radionuclide source modelation

### Image Reconstruction
- CASToR tools and configurations - gui interface for CASToR reconstruction tools and converter of CASToR interfile format to NIfTi (reference: https://github.com/miguelleaolopes/HiRezBrainPET_git?tab=readme-ov-file#bpet_castor_v311-folder which code was used as a starting point to build a more friendly user interface for CASToR recosntruction of GATE PET list-mode files
- PyTomography scripts - adaptations to PyTomography source files for compatibilty with scanner model, Deep Image Prior (DIP) reconstruction and main reconstruction files
- PET Reconstruction analysis results - includes the CASToR and PyTomography simulated PET reconstruction image analysis results, analysis and compararion with ground-truth PET image  

### MC Dosimetry
- Dosimetry calibration tool - Calibrates GATE's output absorbed dose distribution according to Y90 radioactive decay over time and patient's administrated 
    activity of Y90 and other treatment specific data
- MC-GATE Statistical uncertainty tool - MC dosimetry statistical uncertainty in GATE for each VOI in analysis and the PTV threshold of $\overline{SU} < 2\%$ should be achieved in voxels receiving absorbed doses $D_k > 80 \ \text{Gy}$ within the PTV to ensure sufficient dosimetry accuracy. Therefore, the total number of primaries was initially set to 10 million. If the threshold $\overline{SU}_{D_k > 80 \ \text{Gy}}$ was not met, a custom SU calculator was used to automatically estimate the number of primaries required for the simulation to reach the target $\overline{SU}$.
- Absorbed dose analysis - DVHs and dose bar plots computation 

An explaination on each folder content files can be found on what each file README is specifically for.

## Credits
If you find this code useful, please consider citing:

> Ornelas, B. (2026). *Development of a PET GATE model for voxel-wise dosimetry in radionuclide therapy*. Master’s thesis, Instituto Superior Técnico, Universidade de Lisboa, Lisbon, Portugal.
