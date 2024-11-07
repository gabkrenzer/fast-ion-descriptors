# Do phonons act as an effective descriptor for fast-ion transport?

# Introduction
This repository contains a collection of notebooks and data that investigates correlations between vibrational properties and diffusive properties in solids. More background can be obtained from the chapter *Do phonons act as an effective descriptor for fast-ion transport?* of my [thesis](https://spiral.imperial.ac.uk/handle/10044/1/111142).

The output data obtained by myself running the notebooks presented here can be found in the [data](https://github.com/gabkrenzer/fast-ion-descriptors/tree/main/data) repository

# Preliminary: PhononDB
The phonon data is obtained from the phonon calculation database created by Atsushi Togo. Please refer to (https://github.com/WMD-group/phononDB) to query the phonon data.

# 1. Get data: phonon density of states and phonon descriptors
The notebook `01_get_data.ipynb` contains functions required to organise the phonon density of states \(DOS\) data from PhononDB into a single folder that can be easily worked with later on, as well as functions to calculate phonon descriptors obtained from the DOS data: phonon band-centre, relative spread, DOS first peak, and DOS spectrum featurisation. 

After running `01_get_data.ipynb`, a dataframe `data.csv`, and feature vectors of the DOS \(`viball_feature.npy`, `vibli_feature.npy`, `vibtot_feature.npy`\) are obtained. `data.csv` includes composition data as well as descriptor data for each Li-containing material found in the PhononDB database.

# 2. Labelling conductivities using exisiting conductivity databases
Then, in the `02_labelling_conductivies` notebook, conductivity labels are added to the dataframe using `digitized_data_for_SSEs.csv`, a database obtained from (https://github.com/FALL-ML/materials-discovery), giving the updated dataframe `labelled_data.csv`.

# 3. Investigating correlations between phonon and diffusive properties

## A. High-throughput approach
The labelled data can be visualised in `3aa_visualisation.ipynb`, where fast-ion conducting outliers and candidates can be identified \(`first_peak_candidates.csv`, `pbc_tot_rt_candidates.csv`, `pbc_diff_unknown_*.csv`\). Unsupervised clustering is also attempted in `3ab_clustering.ipynb` and new candidates are identified \(`circle_dos_fv.csv`\). 

M3GNet simulations are then run for all the candidates and more. The data is stored in `stoich.csv`. The results are investigated in `3ac_candidates_investigation.ipynb`.

## B. Direct correlations
M3GNet simulations were finally run for all the materials in the PhononDB database by Kasper Tolborg \(`data_kasper_full.csv`\). Direct correlations between phonon descriptors and diffusivity are investigated in `3b_firect_correlations.ipynb`.

# Appendices

## A. \(Variational\) AutoEncoder
An attempt to reduce the dimensionality of the DOS feature vectors using a \(Variational\) AutoEncoder can be found in `aa_AE.ipynb` and `bb_VAE.ipynb`.

## B. Labelling conductivities using Kasper's dataset
The notebook `b_full_dataset_labelling.ipynb` can be used to create a dataframe, `data_labelled_kasper.csv`, that includes all the dataset with phonon descriptors *and* diffusivity data.

## C. Composition-structure-phonon cross-correlation
A Composition-structure-phonon cross-correlation was also attempted. Composition and structure feature vectors can be obtained using `ca_composition_featuriser.ipynb` and `cb_structure_featuriser.ipynb`, respectively. To run the `cd_csv_corr.ipynb` notebook, the DOS feature vectors must be first converted to `.csv` files using the notebook `cc_npy_to_csv.ipynb`.

# Acknowledgments
This work builds upon the work of Amelia Hu realised as part of a UROP summer internship. Her original work can be found at (https://github.com/AmeliaHu0920/urop-project). The internship was co-supervised by Anthony Onwuli and myself.

The data `data_kasper_full.csv` and `stoich_data.csv` was obtained by Kasper Tolborg using M3GNet.
