# XRD Data Processing Pipeline

This file describes the pipeline to convert XRD data acquired in IMM-CT unit of NFFA-DI to a NeXus-compliant format. The following files in this repository are related:

- `XRD_IMM-CT_readme.md`: This file. Describes the Data Processing Pipeline.
- `XRD_IMM-CT_script.ipynb`: Converts .uxd XRD measurement files into NeXus-like structured hdf5 files (.nxs).
- `60C_air_15_1ass1_axssoll_035sci_2tho_1_normalized.uxd`: Example data file produced by the XRD instrument.
- `XRD_CNR-IMM@CT_output.nxs`: Example output file of the Data Processing Pipeline.
- `XRD_CNR-IMM@CT_NXxrd_bru.nxdl.xml`: Describes the NeXus-compliant file structure.

Note of file naming convention:\
Because the measurment filename contains important metadata, it does not have the prefix XRD_CNR-IMM@CT. Filename is partially composed of regular expressions and parsed by the script.

## Files description

### 1. `XRD_IMM-CT_script.ipynb`

**Purpose**: Converts experimental data from bruker's universal xrd  text format (.uxd) file into a structured .nxs file.

**Input**:
- Measurement .uxd file

**Output**:
- Output .nxs file: NeXus-like hdf5 file.

**Instructions**:

- Edit user-input fields in dedicated Jupyter cell
- Run as a Jupyter Notebook

**Requirements**:

Required packages:
```bash
pip install numpy==1.26.4
pip install h5py==3.11.0
```
Tested in Python 3.11

### 2. `XRD_IMM-CT_NXxrd_bru.nxdl.xml`

**Purpose**: 
- Describe a NeXus-compliant definition for XRD and XRR measurements, tailored around the facility in CNR IMM Catania.
- Formatted for NeXus documentation, for future sharing with the NeXus community.

---

## Workflow Summary

1. **Convert uxd to nxs**  
   ➤ `XRD_IMM-CT_script.ipynb`

---

## Requirements

Required packages:
```bash
pip install numpy==1.26.4
pip install h5py==3.11.0
```
Tested in Python 3.11

---

## Notes
