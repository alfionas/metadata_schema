# ELLIPSOMETER Data Processing Pipeline

This file describes the pipeline to convert ellipsometry data acquired in IMM-CT unit of NFFA-DI to the NeXus format application definition NXellipsometry. The following files in this repository are related:

- `ELLIPSOMETER_IMM-CT_readme.md`: This file. Describes the Data Processing Pipeline.
- `ELLIPSOMETER_IMM-CT_script.ipynb`: Converts .dat ELLIPSOMETER measurement files into NeXus NXellipsometry hdf5 files (.nxs).
- `ELLIPSOMETER_CNR-IMM@CT_input.dat`: Example data file produced by the ELLIPSOMETER instrument.
- `ELLIPSOMETER_CNR-IMM@CT_ELN.ods`: Open Document spreadsheet to be used as ELN in conjunction with the script.
- `ELLIPSOMETER_CNR-IMM@CT_ELN.xlsx`: Excel spreadsheet to be used as ELN in conjunction with the script.
- `ELLIPSOMETER_CNR-IMM@CT_output.nxs`: Example output file of the Data Processing Pipeline.

## Files description

### 1. `ELLIPSOMETER_IMM-CT_script.ipynb`

**Purpose**: Converts experimental data from a text (.dat) file into a structured .nxs file.

**Input**:
- Spreadsheet {.ods, .xlsx} ELN file
- Identifier for spreadsheet row within Jupyter notebook cells.
- Measurement .dat file

**Alternative input**
- User input metadata directly within Jupyter notebook cells
- Measurement .dat file

**Output**:
- Output .nxs file: NXellipsometry file.

**Instructions**:

- Fill spreadsheet ELN
- Edit user-input fields in dedicate Jupyter cell
- Run as a Jupyter Notebook

**Requirements**:

Required packages:
```bash
pip install numpy==1.26.4
pip install pandas==2.2.2
pip install openpyxl==3.1.5
pip install odfpy==1.4.1
pip install h5py==3.11.0
```
Tested in Python 3.11

### 2. `ELLIPSOMETER_IMM-CT_ELN{.ods,.xlsx}`

**Purpose**: 
ELN and user-input metadata

**Instructions**:
Fill one row with all the information regarding the measurement
- Identificatore is required and must be unique within the column
- Filepath is required and must be a relative filepath to script cwd
- If Output File is left empty, 'output.nxs' is used as default

The remaining columns are optional, with the following notes for NeXus compliance
- Data Ellissometria should always be in dd/mm/yyyy format  
- Formula Chimica should follow the Hill system (https://en.wikipedia.org/wiki/Chemical_formula#Hill_system)
- Operatore can be omitted, but if specified it must match a unique row in the Operatori worksheet.

pandas.read_excel assumes . as a decimal separator and no thousands separator, so be sure to have the correct locale settings for open documents or microsoft office, or to adjust pandas.read_excel with the arguments "thousands" (default "None") and "decimal" (default ".") within the script.

**Alternative**
Alternatively, user input can be specified within the script directly in a dedicated Jupyter cell. However doing so is not recommended as it skips compiling the ELN.

---

## Workflow Summary

1. **Fill ELN**  
   ➤ `ELLIPSOMETER_IMM-CT_ELN.{ods,xlsx}`
2. **Convert dat to nxs**  
   ➤ `ELLIPSOMETER_IMM-CT_script.ipynb`

---

## Requirements

Required packages:
```bash
pip install numpy==1.26.4
pip install pandas==2.2.2
pip install openpyxl==3.1.5
pip install odfpy==1.4.1
pip install h5py==3.11.0
```
Tested in Python 3.11

---

## Notes
