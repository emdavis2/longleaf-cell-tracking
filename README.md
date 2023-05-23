Cell Tracking on UNC Longleaf Cluster
================
## Quick Summary:
This repo contains code to perform cell tracking and tracking quality control of segmented images of JR20 dermal fibroblast cell DIC images. This code is run on the UNC Longleaf cluster using Open OnDemand (https://help.rc.unc.edu/ondemand). Here is a quick overview of the files in this repo and what they do:

`libraries` is a folder that contains python scripts of functions used in the `Unified_Tracking_and_Shape_Notebook.ipynb` notebook.

`Unified_Tracking_and_Shape_Notebook.ipynb` is a Jupyter notebook that uses binary masks to track cells, and then plots the tracks in movies to allow the user to evaluate performance and perform quality control. The outputs of this notebook are the x, y coordinates of cell positions in each track (`tracks.pkl`), a folder of cell masks that are associated with each track (`tracks_masks`), and a dictionary of dataframes that has cell shape information for each frame in the tracks (`tracks_shape.pkl`). The parameters used for the analysis are saved in a folder called `AnalysisParameters`.

## Set up to run code:
Clone this repository to your home directory on the Longleaf cluster. You must create a conda environment and kernal to run this notebook. To do this, change directory to the newly cloned repo (where the `cell_tracking.yaml` file is located) and run:

```
conda env create --file cell_tracking.yaml
```

Once the environment is done installing all the packages, run `conda activate cell_tracking`. Next, we must create a kernal corresponding to the newly created conda environment. To do this, run:

```
python -m ipykernel install --user --name cell_tracking --display-name "Python cell_tracking"
```

Now, the kernal should be created and should be visible when running Jupyter notebook on Open OnDemand.

## Workflow for a dataset:

In order to perform cell tracking, there must be binary masks of cell membrane and nucleus for the dataset you wish to perform tracking on. If there are no binary masks for the dataset, you can use the code in the Longleaf segmentation repository (https://github.com/emdavis2/longleaf-cell-segmentation) to segment the data.

To run the `Unified_Tracking_and_Shape_Notebook.ipynb`, go to UNC Open OnDemand (https://help.rc.unc.edu/ondemand), login and start a Jupyter Notebook interactive session. Make sure to request enough time (I recommend 8 hours to be safe), request just 1 CPU, and in the Additional Job Submission Arguments section enter `--mem=10gb`. Once the job is submitted it should be ready within 2-3 minutes. Once the job is ready in the queue, click "Connect to Jupyter" and navigate to the directory of this repository on your Longleaf home directory and open the `Unified_Tracking_and_Shape_Notebook.ipynb` notebook. Make sure you are connected to the `Python cell_tracking` kernal. Run the notebook cell by cell, modifying the variables that need to be modified as indicated in the notebook (namely the paths to the raw images and masks as well as the directory and name of the folder to save the outputs to). 