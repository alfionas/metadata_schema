# PVD-MS Data Processing Pipeline

This file describes the pipeline to produce Nomad ELN for Physical Vapor Deposition - Magnetron Sputtering (PVD-MS) synthesis performed in IMM-CT unit of NFFA-DI. 

The pipeline assumes that the Nomad plugin at the following GitHub repository is installed:
https://github.com/lsal93/Fabrication-utilities/tree/7b6e56be9ffd0c241b9f957d4dd5db0c4941dfd2

The following files in this repository are related:

- `PVD-MS_cnr-imm.ct_readme.md`: This file. Describes the Data Processing Pipeline.
- `PVD-MS_cnr-imm.ct_ELN.archive.json`: Example Nomad ELN for a PVD-MS process.
- `PVD-MS_cnr-imm.ct_equipment.archive.json`: Example equipment entry for PVD-MS, and entry for PVD-MS equipment at Catania IMM.

---

## Nomad plugin information

This pipeline assumes that the Nomad plugin at the following GitHub repository is installed:
https://github.com/lsal93/Fabrication-utilities/tree/7b6e56be9ffd0c241b9f957d4dd5db0c4941dfd2

The plugin is a minor customization of https://github.com/Trog-404/Fabrication-utilities developed by Matteo Bontorno as his thesis for NFFA-DI Master in Data Management and Curation.
https://doi.org/10.5281/zenodo.15878149
Specifically, it is based on the following commit:
https://github.com/Trog-404/Fabrication-utilities/tree/6406d2441c2136881696e23302bea818b1ae8882

The CVD classes specified with the suffix '_catania' are adapted from the original plugin with minimal modifications, and are intended to be compatible with the original classes.

The Sputtering classes are based on the CVD ones taken as a template, but they are new and not compatible with the sputtering class of the original plugin.

The plugin has been tested in a local OASIS running in a PC.

---

## Workflow Summary

0. **Make an equipment entry**  
   Before making an ELN entry, the relative equipment should be already present in Nomad. In principle, equipment informations need to be entered only once.
1. **Make an ELN entry**
2. **(Optional) load processing monitor file**
   The machine may provide a file with the time traces of readings from several sensors and recipe setpoints.\\
   It might be appropriate to use settings that produce relatively small process monitor files. Alternatively, it might be appropriate to compress such files by any combination of the following strategies: undersample the data; truncate data to e.g. first decimal place; use compressed formats like .zip. See following section for an example Python-based compression script.

### Example compression script

The following is an example of a compression strategy for large process-monitoring files, based on facilities at Catania IMM. 

```bash
import numpy as np
import pandas as pd

# parameters for compression
threshold = 1.5
smooth_window=5
dec_places=1
zip=TRUE

df = pd.read_csv(filedialog.askopenfilename())

for col in df.columns:
    
    #skip time column
    if col == 'time_ms':
        continue

    #boxcar smoothing
    compressed_df[col] = compressed_df[col].rolling(window=smooth_window, min_periods=1, center=True).mean()

    #set values below threshold to 0
    mask = np.abs(compressed_df[col]) < threshold
    compressed_df.loc[mask, col] = 0
    if mask.all():
        compressed_df[col] = compressed_df[col].astype(int)

if ZIP:
   #save zipped directly
   compressed_df.to_csv('compressed.csv.zip', index=False, float_format='%.'+str(dec_places)+'f', compression="zip")
else:
   # save to csv with a single decimal point
   compressed_df.to_csv('compressed.csv', index=False, float_format='%.'+str(dec_places)+'f')
```
---

## Requirements

Plugin must be installed in Nomad.

---

## Notes
