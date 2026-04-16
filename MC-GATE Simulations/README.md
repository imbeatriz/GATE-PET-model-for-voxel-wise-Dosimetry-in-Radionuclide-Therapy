## MC-GATE Simulations

Two types of MC-GATE simulations were performed: 

- **PET simulations**: Performed using the implemented **GATE PET model** (digital twin of the Philips Vereos PET/CT scanner). PET acquisition simulations using a patient-specific phantom and a non-uniform ⁹⁰Y activity distribution derived from the patient’s PET image (ground-truth PET).

- **MC dosimetry**: Performed using ground-truth and simulated PET images as ⁹⁰Y activity distribution sources. GATE simulates absorbed dose deposition in a patient-specific phantom using the corresponding non-uniform ⁹⁰Y activity distributions, allowing later comparison between the dosimetry results.

### Y90 Positron Energy Spectrum

Defining the positron emission from ⁹⁰Y in GATE is challenging, as neither GEANT4 or the DECDATA database includes the minor positron branching ratio associated with the $0^+ \rightarrow 0^+$ transition. 

To address this limitation, the ⁹⁰Y positron activity source was modeled using a theoretically estimated continuous positron energy spectrum based on internal pair production (IPP) (Dryák *et al.*, [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0969804319303689)).

<p align="center">
  <img src="https://github.com/user-attachments/assets/527fc989-ea6d-4bc7-918a-ec4716415af5" width="400" />
</p>

<p align="center">
  <em>Figure 1 – ⁹⁰Y positron spectrum</em>
</p>

**The following code was developed:**

- **[Y90_positron_spectrum_generator_for_GATE.ipynb](./Y90%20Positron%20Energy%20Spectrum/Y90_positron_spectrum_generator_for_GATE.ipynb)** – Notebook that generates and visualizes an approximate ⁹⁰Y positron energy spectrum using a parabolic model. The spectrum is numerically normalized over the 0–739 keV range to ensure a valid probability distribution. The resulting energy–probability pairs are exported to a text file with *linear interpolation* mode and can be directly used in GATE for the radionuclide source definition. Update the output directory path in the script before execution.

- **[Y90_positron_spectrum_generator_keV_to_MeV_GATE.txt](./Y90%20Positron%20Energy%20Spectrum/Y90_positron_spectrum_generator_keV_to_MeV_GATE.txt)** – Example of a generated spectrum file formatted for use in MC-GATE simulations.

### MC-GATE Simulation Files

**This folder contains all macros scripts used for the MC-GATE simulations performed in this work:**

- **[Y90_MCDosimetry_Simulation_digitalPhantom.mac](./MC-GATE%20Simulation%20Files/Y90_MCDosimetry_Simulation_digitalPhantom.mac)** – MC dosimetry simulation using digital phantom as the patient-specific model, with non-uniform ⁹⁰Y activity distribution and ⁹⁰Y electron spectrum from the DECDATA database.

- **[Y90_MCDosimetry_Simulation_HU.mac](./MC-GATE%20Simulation%20Files/Y90_MCDosimetry_Simulation_HU.mac)** – MC dosimetry simulation using HU phantom, incorporating non-uniform ⁹⁰Y activity distribution and the DECDATA ⁹⁰Y electron spectrum.

- **[Y90_MCPET_Simulation_Vereos.mac](./MC-GATE%20Simulation%20Files/Y90_MCPET_Simulation_Vereos.mac)** – GATE PET model simulation. Digital twin of the Philips Vereos PET/CT system, using patient-specific phantom and non-uniform ⁹⁰Y activity distribution derived from the patient’s PET image.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e74e18d3-98cb-422b-b2b2-3f4da5b5e5d5" width="400" />
</p>

<p align="center">
  <em>Figure 1 – GATE PET model</em>
</p>

- **[Normalization_MCPET_Simulation_Vereos.mac](./MC-GATE%20Simulation%20Files/Normalization_MCPET_Simulation_Vereos.mac)** – Simulation used to generate a PET scanner calibration scan for normalization correction in PET image reconstruction. This setup includes an auxiliary PET acquisition using a thin annular phantom filled with Fluor-18 designed to cover all possible lines of response (LORs).

<p align="center">
  <img src="https://github.com/user-attachments/assets/d190d6a8-dfec-4905-a360-efe9b39d5aec" width="600" />
</p>

<p align="center">
  <em>Figure 2 – Normalization simulation setup</em>
</p>

- **[Y90_MCDosimetry_Simulation_PETsimulated.mac](./MC-GATE%20Simulation%20Files/Y90_MCDosimetry_Simulation_PETsimulated.mac)** – MC dosimetry simulation using HU phantom and simulated PET ⁹⁰Y activity distribution from the GATE PET model, with the DECDATA ⁹⁰Y electron spectrum.

#### Additional Folders

- **data** – Contains all required input files for MC-GATE simulations, including material definitions, tissue properties, density calibration files (specific calibration files `GEMINIDensitiesTable.txt` and `GEMINIMaterialsTable.txt`), and ⁹⁰Y electron and positron energy spectra.

- **mac** – Includes auxiliary macro files used by the main simulation scripts, particularly for defining the GATE PET model and scanner geometry.

### GATE 9.2 Parallel Jobs Tools

Tools for splitting MC-GATE simulations into multiple smaller jobs and executing them in parallel using Python multiprocessing, significantly reducing computation time by leveraging multiple CPU cores. 

**The following code was developed:**

- **[GATE_Parallel_Job_Splitter&Runner.py](./GATE%209.2%20Parallel%20Jobs%20Tools/GATE_Parallel_Job_Splitter&Runner.py)** - This script automatically divides a MC-GATE simulation into multiple smaller jobs and executes them in parallel. Each job gets its own time window, unique output names, and separate log files.

    **Usage Example:**
    ```bash
    python3 gate_parallel_runner.py mySimulation.mac ./output 30 120
    ```

<p align="center">
  <img src="https://github.com/user-attachments/assets/4832c1b9-328b-43f9-a5dc-ee48fa5e6de5" width="48%" />
  <img src="https://github.com/user-attachments/assets/7bf4685c-1b22-4943-8577-595fda58f16d" width="48%" />
</p>

<p align="center">
  <em>Figure 1 – GATE parallel job tool usage overview &nbsp;&nbsp;&nbsp;&nbsp; Figure 2 – Example execution of the parallel job tool</em>
</p>

- **[GATE_ROOT_Files_Merger.py](./GATE%209.2%20Parallel%20Jobs%20Tools/GATE_ROOT_Files_Merger.py)** - This script merges multiple GATE ROOT output files in a folder into a single ROOT file.

    **Usage Example:**
    ```bash
    python3 merge_root_files.py ./output merged_simulation.root 
    ```
<p align="center">
  <img src="https://github.com/user-attachments/assets/e94d9550-4395-4293-80ed-5d8a08e2c03f" width="600" />
</p>

<p align="center">
  <em>Figure 1 – GATE ROOT file merger tool usage overview</em>
</p>

