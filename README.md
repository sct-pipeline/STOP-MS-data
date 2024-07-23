# STOP-MS-data

Processing pipeline to compute CSA on upper spinal cord on MPRAGE from large MS cohort from Karolinska Institute. The MPRAGE are brain scans from which a small chunk of the spinal cord is visible (typically C2-C3), and is used to compute CSA. 

## Requirements

### Following dependencies are required
- SCT version 6.3 ([Install Spinal Cord Toolbox](https://spinalcordtoolbox.com/user_section/installation.html))
- [Install manual-correction](https://github.com/spinalcordtoolbox/manual-correction?tab=readme-ov-file#2-installation) : the SCT command for the vertebral labeling doesn't work for some subjects in the dataset (the identification of the levels is wrong), therefore it will be necessary to fix it manually for subjects who fail the vertebral labeling.


### Config YAML file

A config YAML file, as shown below, is needed to precise the path to the dataset and the path to save the output files. 
```
# Path to the folder containing the dataset 
path_data: 

# Path to save the output
path_output:

```

It is also necessary to create a main folder containing the dataset folder, the script and the config YAML file. Organisation within the main folder should look like this:

```bash
├── DATA
└── config.yml
```


## How to use the script

### First step 

Run processing across all subjects : 

```bash
cd PATH/TO/THE/MAIN/FOLDER

#To allow permissions 
chmod +x config.yml 
  
#SCT command to run the script across all subjects
sct_run_batch -script process_data.sh -config config.yml -jobs 9
  ```

### Second step

Launch the QC report and flag with a ❌ the subjects that need to be manually corrected for the vertebral labeling and download the config YAML file that list all the subjects 
which failed.

Then perform manual vertebral labeling as shown in the following video tutorial :

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/IgJUu5CCHxY/0.jpg)](https://www.youtube.com/watch?v=IgJUu5CCHxY)


### Third step 

Rerun the script as in the second step. For each subject, if the manual correction exists, it will use it. If not, it will regenerate the vertebral labeling.

