# Data Version Control (DVC) Directory

This directory incorporates Data Version Control (DVC) to manage and version control data in our **Data Science Project Template**. DVC is an open-source tool designed to handle large files, data sets, machine learning models, and metrics as well as to enable data sharing and synchronization in a Git-like fashion.

## Structure

- `dvc/`: This sub-directory holds all data tracked by DVC.
- `dvc/data/`: This sub-directory contains the raw data files.
- `dvc/data/raw/`: This sub-directory contains the raw data files.
- `dvc/data/processed/`: This sub-directory contains the processed data files.
- `dvc/results/`: This sub-directory contains the results of the analysis.

## How to Use DVC

1. **Adding Data:** Add your data to DVC:

```bash
dvc add dvc/data/raw_data.csv
```

2. **Committing to DVC:** Once the data is added, a `.dvc` file is created. You need to commit this file to track changes:

```bash
git add data/raw_data.csv.dvc
git commit -m "Add raw data"
```

3. **Pushing Data to Remote Storage:** Setup the DVC remote storage to CERN EOS and push your data:

```bash
dvc push
```

## Remote Configuration for CERN EOS

The DVC remote is configured to use CERN's EOS storage. Below is the configuration snippet to be placed in your `.dvc/config` file:

```plaintext
[core]
    remote = eos-cern
['remote "eos-cern"']
    url = ssh://lxplus.cern.ch/eos/project/d/diagbox/dvc/template
    ask_password = true
```

With this configuration, data inside the `dvc` folder will be uploaded to CERN EOS when `dvc push` is executed.

______________________________________________________________________

Utilizing DVC in our project helps to maintain a clear and trackable record of our data, which is essential for reproducibility and collaboration. It also facilitates secure storage and sharing of data through CERN's EOS storage system.
