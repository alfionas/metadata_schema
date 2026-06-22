# SRP Data Processing Pipeline

This file describes the pipeline to convert Spreading Resistance Profiling (SRP) data acquired in IMM-CT unit of NFFA-DI in a NeXus-compliant format. The following files in this repository are related:

- `SRP_IMM-CT_readme.md`: This file. Describes the Data Processing Pipeline.
- `SRP_IMM-CT_script.ipynb`: Converts .ASC SRP measurement files into NeXus-like structured hdf5 files (.nxs).
- `SRP_IMM-CT_NXspreading.nxdl.xml`: Describes the NeXus-compliant file structure.
- `SRP_CNR-IMM@CT_input.ASC`: Example data file produced by the SRP instrument.
- `SRP_CNR-IMM@CT_output.nxs`: Example output file of the Data Processing Pipeline.

## Files description

### 1. `SRP_IMM-CT_script.ipynb`

**Purpose**: Converts experimental data from an ASCII file into a structured .nxs file.

**Input**:
- User provided input and output file names within the Jupyter notebook cells.
- Measurement .ASC file,

**Output**:
- Output .nxs file: NeXus-like hdf5 file.

**Instructions**:

- Edit user-input fields
- Run as a Jupyter Notebook

**Requirements**:

Required packages:
```bash
pip install numpy==1.26.4
pip install h5py==3.11.0
```
Tested in Python 3.11

### 2. `SRP_IMM-CT_NXspreading.nxdl.xml`

**Purpose**: 
- Describe a NeXus-compliant definition for Spreading Resistance Profilometry measurements, tailored around the facility in CNR IMM Catania.
- Formatted for NeXus documentation, for future sharing with the NeXus community.

---

## Workflow Summary

1. **Convert ASC to nxs**  
   ➤ `SRP_IMM-CT_script.ipynb`

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
