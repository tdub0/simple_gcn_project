# Simple GCN Project

This is a re-implementation of the SGC described in [Simplifying Graph Convolutional Networks](https://arxiv.org/abs/1902.07153) from ICML2019. The main goal of this project is to verify the claims from the paper and extend the experiements on SGC and GCN across several page-page datasets.

# How to Run the Experiments in Google Colab
- Download the datasets in the `Datasets` section.
- Upload `simple_gcn_project.ipynb` to a Google Colab instance, preferably from Google Drive.
- Mount the datasets to the Google Colab instance; this can be done easily through Google Drive and Section 2 in the notebook.
- Change the runtime type to `T4`.
- Connect to a hosted `T4` runtime.
- Run the following Sections in the notebook to setup the environment, configure the models, and load necessary functions:
    - Section 1: Global Dependencies.
    - Section 2: Mount Datasets *if not already done*.
    - Section 3: Random Seed.
    - Section 4: Models.
    - Section 5: Normalization.
    - Section 6: Analysis.
    - Section 7: Loading Datasets *if running Citation Network tests*.
    - Section 8: Train & Test Functions.
    - Section 9: Results Handling.
    - Section 11: Extended Dataset Loading *if running Extended Dataset tests*.
- Run the following Sections in the notebook to run tests:
    - Section 10: Citation Network Testing for SGC and GCN *if running Citation Network tests*.
    - Section 12: Extended Dataset Testing on SGC *if running Extended Dataset tests*.
    - Section 13: Extended Dataset Testing on GCN *if running Extended Dataset tests*.
- Wait for the tests to finish.

# Code Structure

# Code Source Description
- [ ] Which code files have been copied from other repositories with references to these repositories
- [ ] Which code files have been modified and how they have been modified
- [ ] Which code files are the student's original code.

# Datasets

Cora and Pubmed - Citation Networks
The original dataset source can be found at [tkipf/gcn:gcn/data](https://github.com/tkipf/gcn/tree/master/gcn/data).
The dataset used for this project can be found at [Tiiiger/SGC:data](https://github.com/Tiiiger/SGC/tree/master/data).

Cornell, Texas, Wisconsin can be found at [bingzhewei/geom-gcn:new_data](https://github.com/bingzhewei/geom-gcn/tree/master/new_data).
Chameleon can be found at [chennnM/GCNII:new_data/chameleon](https://github.com/chennnM/GCNII/tree/master/new_data/chameleon).
Combine the `new_data` folders to have a single `new_data` folder with all four datasets.
