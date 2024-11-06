# Do phonons act as an effective descriptor for fast-ion transport?

# Introduction
This repository contains a collection of notebooks and data that investigate correlations
between vibrational properties and diffusive properties in solids. The outputs obtained by myself can be found in the [data](https://github.com/gabkrenzer/fast-ion-descriptors/tree/main/data) repository. More background can be obtained from the last Results Chapter of my [thesis](https://spiral.imperial.ac.uk/handle/10044/1/111142).

# Preliminary: PhononDB
Phonon data is obtained from the phonon calculation database created by Atsushi Togo. Please refer
to (https://github.com/WMD-group/phononDB) to query the phonon data.

# 1. Get data: phonon density of states and phonon descriptors
The notebook `01_get_data.ipynb` contains functions required to organise the phonon density of
states \(DOS\) data from PhononDB into a single folder, as well as functions to calculate phonon descriptors obtained from the DOS data: phonon band-centre, relative spread, DOS first peak, and DOS spectrum featurisation. 

After running `01_get_data.ipynb` a dataframe `data.csv`, and feature vectors for the DOS \(`viball_feature.npy`, `vibli_feature.npy`, `vibtot_feature.npy`\) are obtained. `data.csv` includes composition data as well as descriptor data for each Li-containing material found in the PhononDB database.

# 2. Labelling conductivities using exisiting conductivity databases
Then, in the `02_labelling_conductivies` notebook, conductivity labels are added to the dataframe using `digitized_data_for_SSEs.csv`, a database obtained from (https://github.com/FALL-ML/materials-discovery).

# 3. Investigating correlations between phonon and diffusive properties

## A. High-throughput approach
The labelled data is first visualised in `3aa_visualisation.ipynb` and fast-ion conducting outliers are identified. Unsupervised clustering is also attempted in `3ab_clustering.ipynb`. Different candidates are obtained from the visualisation and the clustering. The candidates are then fully investigated in M3GNet simulations. The results are investigated in `3ac_candidates_investigation.ipynb`.

## B. Direct correlations
M3GNet simulations were ran for all the materials in the PhononDB database by Kasper Tolborg \(`data_kasper_full.csv`\). Direct correlations between phonon descriptors and diffusivity are investigated in `3b_firect_correlations.ipynb`.

# Appendix

## A. \(Variational\) AutoEncoder
An attempt to reduce the dimensionality of the DOS feature vectors using a \(Variational\) AutoEncoder can be found in `aa_AE.ipynb` and `bb_VAE.ipynb`.

## B. Labelling conductivities using Kasper's dataset

## C. Composition-structure-phonon cross-correlation

# Acknowledgments
This work builds upon the work of Amelia Hu realised as part of a UROP summer internship. Her original work can be found at (https://github.com/AmeliaHu0920/urop-project). The internship was co-supervised by Anthony Onwuli and myself.
