# Table of Contents

1. [Introduction](#introduction)
   - [Installation](#installation)
   - [NeXus](#nexus)
2. [Workflow Steps](#workflow-steps)
   - [User Input](#user-input)
   - [Reading FIB Files](#reading-fib-files)
   - [Parsing into the Output Format](#parsing-into-the-output-format)
   - [Validating the Output File](#validating-the-output-file)

## Introduction

The script is designed as a Jupyter Notebook (`FIB_CNR-IMM@CT_script.ipynb`) to be simple and intuitive and easy to use. 

Only the “USER INPUT” section of the script is intended to be edited by the user. This section contains the configuration parameters required to specify the data file paths and to access the Electronic Laboratory Notebook (ELN). Please note that this script can only be executed within the institutional network. The Electronic Laboratory Notebook (elabFTW) referenced by the script is accessible exclusively via the local institutional internet infrastructure and cannot be reached from external networks. Attempting to run the script outside the institutional environment will prevent access to the ELN and will result in execution failure.

The final stage of the workflow includes validation of the generated output using punx.

### Installation

To use the parser, copy the notebook file into your working directory. 

The script was developed and tested with Python 3.11.9, numpy 1.26.4, h5py 3.11.0, tifffile 2023.4.12, punx 0.3.5 and jupyter notebook support. In addition, the script uses the subprocess and os modules from the Python standard library. For optional output validation, punx 0.3.5 and requests 2.32.3 are required.

### NeXus

NXem is an "application definition" within the NeXus standard designed to describe the components of an electron microscope (EM), including focused ion beam (FIB) capabilities when available.

The NeXus documentation and the specific version of the NXem definition implemented by this script can be found at https://www.nexusformat.org/ and https://github.com/nexusformat/definitions/blob/v2025.11/applications/NXem.nxdl.xml.

## Workflow Steps

Before starting the laboratory session, it is mandatory to complete the elabFTW template associated with the experiment. This step is essential to ensure traceability, reproducibility, and proper documentation of the experimental data.

As a Jupyter Notebook, the script is divided into code and markdown cells, which are referenced throughout this documentation. The initial cell is dedicated to importing the required Python packages.

### User Input

Once the elabFTW instance is available and the corresponding template has been completed, the following information must be provided in the “USER INPUT” section of the script: 
   - Univocal authentication number of the user, required for access to the local elabFTW system.
   - Experimental session URL and the corresponding session identification number.
   - Correct directory path to the folder containing the data files to be processed.

### Reading FIB Files

A laboratory session typically generates a large number of TIFF image files, which are stored during the acquisition process. These files represent sequential experimental outputs and must be processed in a consistent and reproducible manner.

This part of the script is specifically designed to:
   - Chronologically sort the TIFF files based on their acquisition time, ensuring that the original experimental sequence is preserved.
   - Define and manage dedicated functions to load each image file and extract the corresponding metadata, allowing correct interpretation of acquisition parameters and experimental conditions.

### Parsing into the Output Format

The acquired data and associated metadata are converted into the required NXem-compliant NeXus format. This conversion is performed using the h5py library and follows the structure defined by the NXem application definition.

### Validating the Output File

The resulting NeXus file is validated using punx to ensure compliance with the NXem specification.

