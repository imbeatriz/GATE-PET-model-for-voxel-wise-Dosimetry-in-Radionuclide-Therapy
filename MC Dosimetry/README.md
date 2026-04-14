## MC Dosimetry 

MC dosimetry results were analyzed based on the absorbed dose distribution maps (in Gy), with particular focus on the mean absorbed dose within each VOI.

Simulations were performed using both ground-truth and simulated PET images as ⁹⁰Y activity distribution sources, allowing comparison of dosimetry results derived from each input with the voxel S-value (VSV) method.

### Dosimetry Calibration Tool

The absorbed dose distributions generated from MC dosimetry simulations must be calibrated to account for the physical decay of ⁹⁰Y over time. This calibration allows computation of the final absorbed dose distribution (ADD) corresponding to the patient’s administered activity within the RWLV, while correcting for residual activity and lung shunt fraction.

**The following code was developed:**

- **[ADD_MCGATEoutput_CalibrationTool.py](./MC%20Dosimetry/ADD_MCGATEoutput_CalibrationTool.py)** – Tool for calibrating absorbed dose distributions by accounting for ⁹⁰Y radioactive decay, administered activity, residual activity, and lung shunt fraction.

<p align="center">
<img width="679" height="313" alt="Screenshot from 2026-03-13 10-18-35" src="https://github.com/user-attachments/assets/43f893a5-535d-4ae8-a247-c85046093207" />
</p>

<p align="center">
  <em>Figure 1 – MC Dosimetry calibration Tool for RE</em>
</p>

### MC-GATE Dosimetry Statistical Uncertainty Tools

Tools for estimating statistical uncertainty (SU) in MC-GATE simulations for each VOI associated to the absorbed dose distribution. 

**The following code was developed:**

- **[PTV_AD_thresholdSU_calculator.ipynb](./MC-GATE%20Dosimetry%20Statistical%20Uncertainty%20Tools/PTV_AD_thresholdSU_calculator.ipynb)** – Custom tool for estimating the required number of simulated primaries to achieve a target SU in MC dosimetry. Based on recommended practices, it enforces $\overline{SU} < 2\%$ within the PTV for voxels receiving absorbed doses $D_k > 80\,\text{Gy}$, ensuring adequate dosimetric accuracy in RE simulations.

- **[VOI_AD_SU_calculator.ipynb](./MC-GATE%20Dosimetry%20Statistical%20Uncertainty%20Tools/VOI_AD_SU_calculator.ipynb)** – Tool for calculating SU of the mean absorbed dose for each VOI.

<p align="center">
  <img src="https://github.com/user-attachments/assets/65d13b91-9fc3-4e85-a45a-bd5a2de71816" width="48%" />
  <img src="https://github.com/user-attachments/assets/692f0c60-880c-4c78-95f2-c9b778c580fd" width="48%" />
</p>

<p align="center">
  <em>Figure 1 – Example execution of the MC statistical uncertainty tool for each VOI in analysis &nbsp;&nbsp;&nbsp;&nbsp; Figure 2 – Example execution for PTV analysis in MC dosimetry ensuring a statistical uncertainty below 2%</em>
</p>

### Dosimetry Analysis

This folder contains the analysis of absorbed dose distributions, including mean absorbed dose estimation for each VOI, dose–volume histograms (DVHs), dose bar distribution plots and a comparision with the VSV method.

**The following code was developed:**

- **[AD_DVHs_digitalphantom_vs_HUphantom.ipynb](./Dosimetry%20Analysis/AD_DVHs_digitalphantom_vs_HUphantom.ipynb)** – Notebook for analyzing and comparing dosimetry results between digital and HU phantoms.

- **[AD_DVHs_simulatedPET_vs_groundtruthPET.ipynb](./Dosimetry%20Analysis/AD_DVHs_simulatedPET_vs_groundtruthPET.ipynb)** – Notebook for comparing dosimetry results obtained from ground-truth and simulated PET images.
