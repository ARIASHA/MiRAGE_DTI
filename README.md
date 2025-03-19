# MiRAGE_DTI
## Overview
This repository contains the code and datasets used in our research paper. The project focuses on drug-target interaction (DTI) prediction using similarity-based methods and feature selection techniques.

We provide:

- Datasets: Preprocessed data, including drug-target mappings, molecular fingerprints, and sequence-based representations.
- Code: Jupyter notebooks that implement similarity calculations, dataset processing, model training, evaluation, and feature selection.

## Repository Structure
### 1. Datasets:

The Datasets folder includes all necessary datasets for running our experiments. The datasets are organized based on Yamanishi’s four benchmark datasets:

- Enzyme
- GPCR (G-Protein-Coupled Receptor)
- Ion Channels
- Nuclear Receptor

Each dataset folder contains:
Drug-Target Mapping: The main dataset that links drugs to their target proteins.
SMILES-Based Features: Features extracted from the SMILES (Simplified Molecular Input Line Entry System) representation of drugs.
Sequence-Based Features: Features derived from protein sequences using k-mers.
Features Folder: Precomputed, ready-to-use feature matrices for our model.


### 2. Code:
The Codes folder contains four Jupyter notebooks corresponding to the four datasets:

- [Enzyme.ipynb](Codes/Enzyme.ipynb)
- [GPCR.ipynb](Codes/GPCR.ipynb)
- [IonChannels.ipynb](Codes/IonChannel.ipynb)
- [NuclearReceptor.ipynb](Codes/NuclearReceptor.ipynb)

#### Notebook Structure
Each notebook follows a structured pipeline:

First, essential libraries such as pandas, numpy, and specialized bioinformatics libraries are imported for similarity calculations. Then, key methods are defined, including functions for similarity calculations, k-mer generation, and feature extraction, each documented with explanations.

Next, datasets are loaded, where drug-target mappings are extracted along with unique drugs and targets. While feature computation is already done and stored in the Datasets folder, this section also outlines the process of computing SMILES similarity, extracting k-mers from protein sequences, and saving computed features as CSV files. 

⚠ Note: These computations can be time-consuming, so they are optional when running the model.

After this, precomputed similarity matrices are loaded for model training. The evaluation process follows, using three different negative sampling ratios:

- 1:1 (Balanced)
- 1:5 (Imbalanced)
- 1:10 (Highly Imbalanced)
For negative sample selection, we randomly choose drug-target pairs from all possible combinations, then split the dataset into train and test sets. The Mirage model is then applied, where features are computed and fed into a Random Forest classifier, results are evaluated, and feature importance is analyzed using Random Forest feature importance ranking.

To enhance performance, we apply feature selection using forward/backward selection. Though computationally expensive, this significantly improves results. The evaluation process is repeated on the optimized feature set.

For statistical validation (only for the 1:1 ratio), we repeat the process 20 times, selecting different negative samples each time. We then perform four statistical tests to compare our 20 results with baseline methods, determining significance based on p-values.

Finally, the evaluation process is repeated for the 1:5 and 1:10 ratios. However, statistical tests are only conducted for 1:1 ratio due to computational constraints.
