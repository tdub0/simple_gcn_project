# Simple GCN Project

This is a re-implementation of the SGC described in [Simplifying Graph Convolutional Networks](https://arxiv.org/abs/1902.07153) from ICML2019. The main goal of this project is to verify the claims from the paper and extend the experiments on SGC and GCN across several page-page datasets.

## How to Run the Experiments in Google Colab

- Download the datasets in the [Datasets](#datasets) section.
- Upload `simple_gcn_project.ipynb` to a Google Colab instance, preferably from Google Drive.
- Mount the datasets to the Google Colab instance; this can be done easily through Google Drive and Section 2 in the notebook.
- Change the runtime type to `T4`.
- Connect to a hosted `T4` runtime.
- Run the following Sections in the notebook to setup the environment, configure the models, and load necessary functions:
  - Section 1: Global Dependencies.
  - Section 2: Mount Datasets _if not already done_.
  - Section 3: Random Seed.
  - Section 4: Models.
  - Section 5: Normalization.
  - Section 6: Analysis.
  - Section 7: Loading Datasets _if running Citation Network tests_.
  - Section 8: Train & Test Functions.
  - Section 9: Results Handling.
  - Section 11: Extended Dataset Loading _if running Extended Dataset tests_.
- Run the following Sections in the notebook to run tests:
  - Section 10: Citation Network Testing for SGC and GCN _if running Citation Network tests_.
  - Section 12: Extended Dataset Testing on SGC _if running Extended Dataset tests_.
  - Section 13: Extended Dataset Testing on GCN _if running Extended Dataset tests_.
- Wait for the tests to finish.

## Code Structure

`simple_gcn_project.ipynb` is structured as 13 distinct sections:

- Section 1: Global Dependencies
  - Dependencies used across most sections.
  - Source: N/A.
- Section 2: Mount Datasets
  - Allows mounting a personal Google Drive to `/content/drive` of the Google Colab environment.
  - Source: N/A.
- Section 3: Random Seed
  - A function to set the `numpy` and `torch` random seeds.
  - Source: [PyTorch Docs: Reproducibility](https://pytorch.org/docs/stable/notes/randomness.html).
- Section 4: Models
  - Models for SGC, GCL, and GCN.
  - Source: Student re-implementation, but written referencing [SGC/models.py](https://github.com/Tiiiger/SGC/blob/master/models.py).
- Section 5: Normalization
  - Functions to convert SciPy sparse matrices to PyTorch tensors, normalize adjacency matrices, and normalize matrix rows.
  - Source: Modified from [SGC/normalization.py](https://github.com/Tiiiger/SGC/blob/master/normalization.py).
- Section 6: Analysis
  - A simple accuracy function.
  - Source: Copied from [SGC/metrics.py](https://github.com/Tiiiger/SGC/blob/master/metrics.py)
- Section 7: Loading Datasets
  - Functions to parse lists from index files to build graph structures, load the citation networks, pre-process the adjacency matrices.
  - Source: Modified from [SGC/utils.py](https://github.com/Tiiiger/SGC/blob/master/utils.py). Removed `citeseer` specific node isolation modifications and adjacency matrix pre-processing out of the citation network loading function for training/testing of GCN.
- Section 8: Train & Test Functions
  - Functions to train and test SGC and GCN with configurable settings. SGC training allows for configurable optimizer; GCN set in the training function to use negative log likelihood loss ([torch.nn.NLLLoss](https://pytorch.org/docs/stable/generated/torch.nn.NLLLoss.html)) due to the configuration mentioned in the original GCN paper.
  - Source: Student written.
- Section 9: Results Handling
  - Function to print out the train and test results in an easy to read table.
  - Source: Student written.
- Section 10: Citation Network Testing for SGC and GCN.
  - This section requires a `sgcn_data` folder with the Cora and Pubmed datasets, see [Datasets](#datasets) for a link to this dataset.
  - The first code section configures the SGC model, imports the dataset, pre-processes the adjacency matrix, trains the model with the cross entropy loss function ([torch.nn.CrossEntropyLoss](https://pytorch.org/docs/stable/generated/torch.nn.CrossEntropyLoss.html)) and the Adam algorithm optimizer ([torch.optim.Adam](https://pytorch.org/docs/stable/generated/torch.optim.Adam.html)), and produces average training time and test accuracy results over 20 runs with 100 epochs each.
  - The second code section configures the GCN model, imports the datasets, trains the model with Adam algorithm optimizer ([torch.optim.Adam](https://pytorch.org/docs/stable/generated/torch.optim.Adam.html)), and produces the average training time and test accuracy results over 20 runs with 100 epochs each.
  - Source: Student written.
- Section 11: Extended Dataset Loading
  - A function to import the extended page-page datasets and random training/validation/testing masks from the specified split file.
  - Source: Modified from [Geom-GCN/utils_data.py](https://github.com/bingzhewei/geom-gcn/blob/master/utils_data.py). Limited down to the four page-page datasets intended for extension tests: Chameleon, Cornell, Texas, and Wisconsin and removed the Geom-GCN specific embedding mode specifications.
- Section 12: Extended Dataset Testing on SGC
  - This section requires a `new_data` folder with Chameleon, Cornell, Texas, and Wisconsin datasets in individual subfolders with those lowercase names, see [Datasets](#datasets) for links to these datasets. This section follows the same configuration as Section 10 for SGC, but runs 10 random splits for training/validation/testing nodes and produces the average training time and test results over 20 runs with 100 epochs each. The post run results are shown for each random split and the overall training time and test accuracy averages.
  - Source: Student written.
- Section 13: Extended Dataset Testing on GCN
  - This section has the same requirement as Section 12 for the `new_data` folder with the page-page datasets stored in correctly named subfolders. This section follows the same configuration as Section 10 for GCN, but runs 10 random splits for training/validation/testing nodes and produces the average training time and test accuracy over 20 runs with 100 epochs each. Post run results are printed for each random split and the overall training time and test accuracy averages, as in Section 12.
  - Source: Student written.

## Datasets

Cora and Pubmed - Citation Networks
The original dataset source can be found at [tkipf/gcn:gcn/data](https://github.com/tkipf/gcn/tree/master/gcn/data).
The dataset used for this project can be found at [Tiiiger/SGC:data](https://github.com/Tiiiger/SGC/tree/master/data).

Cornell, Texas, Wisconsin can be found at [bingzhewei/geom-gcn:new_data](https://github.com/bingzhewei/geom-gcn/tree/master/new_data).
Chameleon can be found at [chennnM/GCNII:new_data/chameleon](https://github.com/chennnM/GCNII/tree/master/new_data/chameleon).
Combine the `new_data` folders to have a single `new_data` folder with all four datasets.
