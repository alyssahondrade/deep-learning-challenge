# deep-learning-challenge
Module 21 Challenge - UWA/edX Data Analytics Bootcamp

Github repository at: [https://github.com/alyssahondrade/deep-learning-challenge.git](https://github.com/alyssahondrade/deep-learning-challenge.git)

## Table of Contents
1. [Introduction](https://github.com/alyssahondrade/deep-learning-challenge/tree/main#introduction)
    1. [Goal](https://github.com/alyssahondrade/deep-learning-challenge/tree/main#goal)
    2. [Repository Structure](https://github.com/alyssahondrade/deep-learning-challenge/tree/main#repository-structure)
    3. [Dataset](https://github.com/alyssahondrade/deep-learning-challenge/tree/main#dataset)
2. [Approach](https://github.com/alyssahondrade/deep-learning-challenge/tree/main#approach)
3. [Analysis](https://github.com/alyssahondrade/deep-learning-challenge/tree/main#analysis)
4. [References](https://github.com/alyssahondrade/deep-learning-challenge/tree/main#references)

## Introduction

### Goal
The purpose of the analysis is to develop a Deep Learning Model that can predict whether applicants will be successful if funded by the nonprofit foundation, Alphabet Soup.

### Repository Structure
The root directory contains:
- `AlphabetSoupCharity.ipynb`, the notebook containing the initial run.
- `AlphabetSoupCharity_Optimisation.ipynb`, the notebook containing the optimised model.
- `helper_functions.ipynb`, the helper functions used in the analysis.
- `Analysis.md`, the report about the process and model.

The following subdirectories:
- `images`, contains all images derived from the analysis.
- `iterations`, contains all the notebooks on model iterations.
- `model`, contains the HDF5 initial and final model files.
- `model/iterations`, contains the HDF5 iteration files.
- `untitled_project` contains the trials used in the hyperparameter tuning.

### Dataset
The dataset used in this analysis is sourced from: [https://www.irs.gov/charities-non-profits/tax-exempt-organization-search-bulk-data-downloads](https://www.irs.gov/charities-non-profits/tax-exempt-organization-search-bulk-data-downloads)

## Approach
1. The initial model was run, as per the notebook instructions.
2. Data preprocessing and feature engineering was explored.
3. Functions were created to simplify the process and minimise repetition.
4. Once the feature engineering phase was exhausted, hyperparameter tuning was introduced.
5. Conducted more optimisation tests, such as dropout and regularization.
6. Created the iteration notebooks in the logical way, to demonstrate thought process concisely.

## Analysis
The complete analysis is available at: [https://github.com/alyssahondrade/deep-learning-challenge/blob/main/Analysis.md](https://github.com/alyssahondrade/deep-learning-challenge/blob/main/Analysis.md)

## References
- [1] How do determine the number of layers and neurons in the hidden layer> [https://medium.com/geekculture/introduction-to-neural-network-2f8b8221fbd3](https://medium.com/geekculture/introduction-to-neural-network-2f8b8221fbd3)

- [2] Encoding Techniques for Machine Learning [https://community.alteryx.com/t5/Data-Science/Encoding-Techniques-for-Machine-Learning-in-Alteryx-A-Concise/ba-p/1203894](https://community.alteryx.com/t5/Data-Science/Encoding-Techniques-for-Machine-Learning-in-Alteryx-A-Concise/ba-p/1203894)

- [3] Layer Activation Functions [https://keras.io/api/layers/activations/](https://keras.io/api/layers/activations/)

- [4] Save, Serialize, and Export Models [https://www.tensorflow.org/guide/keras/serialization_and_saving](https://www.tensorflow.org/guide/keras/serialization_and_saving)

- [5] Keras Dense Layer [https://wandb.ai/ayush-thakur/keras-dense/reports/Keras-Dense-Layer-How-to-Use-It-Correctly--Vmlldzo0MjAzNDY1](https://wandb.ai/ayush-thakur/keras-dense/reports/Keras-Dense-Layer-How-to-Use-It-Correctly--Vmlldzo0MjAzNDY1)

- [6] Regularizer [https://www.tensorflow.org/api_docs/python/tf/keras/regularizers/Regularizer](https://www.tensorflow.org/api_docs/python/tf/keras/regularizers/Regularizer)

- [7] L1 and L2 Regularization Explained [https://spotintelligence.com/2023/05/26/l1-l2-regularization/](https://spotintelligence.com/2023/05/26/l1-l2-regularization/)

- [8] An Introduction to Gradient Boosting Decision Trees [https://www.machinelearningplus.com/machine-learning/an-introduction-to-gradient-boosting-decision-trees/](https://www.machinelearningplus.com/machine-learning/an-introduction-to-gradient-boosting-decision-trees/)
