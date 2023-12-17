# Alphabet Soup Analysis

## Table of Contents
1. [Goal]()
2. [Questions]()
    1. [Data Preprocessing]()
    2. [Compiling, Training, and Evaluating the Model]()
3. [Summary]()
4. [Alternative Solutions]()

## Goal
The purpose of the analysis is to develop a Deep Learning Model that can predict whether applicants will be successful if funded by the nonprofit foundation, Alphabet Soup.

## Questions

### Data Preprocessing
1. What variable(s) are the target(s) for your model?

The target variable for the model is: `IS_SUCCESSFUL`.

2. What variable(s) are the features for your model?

The features from the original dataset are:
- `NAME`, retained as it was observed there were multiple applications per charity.
- `APPLICATION_TYPE`
- `AFFILIATION`
- `CLASSIFICATION`
- `USE_CASE`
- `ORGANIZATION`
- `STATUS`
- `INCOME_AMT`
- `SPECIAL_CONSIDERATIONS`
- `ASK_AMT`

The engineered features are:
- `ORDINAL_INCOME_AMT`, with the `INCOME_AMT` ordinally encoded to account for the missing category: `500000-1M`.
- `LOWER_INCOME`, derived from `INCOME_AMT`.
- `UPPER_INCOME`, derived from `INCOME_AMT`.
- `AFFILIATION_ORGANIZATION`, derived from combining the two columns.
- `AFFILIATION_USECASE`, derived from combining the two columns.

3. What variable(s) should be removed from the input data because they are neither targets nor features?
- `EIN` is neither a target nor feature, as it acts as a primary key for the dataset.

### Compiling, Training, and Evaluating the Model
__1. How many neurons, layers, and activation functions did you select for your neural network model, and why?__

The number of neurons, layers, and activation functions were derived using the hyperparameter tuner.

|Layer|Neurons|Activation Function|
|:---:|:---:|:---:|
|Hidden Layer 1|131|selu|
|Hidden Layer 2|61|relu|
|Output Layer|1|sigmoid|

- The maximum number of neurons per layer was based on a rule of thumb, set to: `number_input_features * 2 - 1`
- The options for the activation function for the hidden layers were:
    - `relu`
    - `leaky_relu`
    - `tanh`
    - `elu`
    - `selu`
    - `exponential`
    - `softmax`
    - `softplus`
- The output layer used a `sigmoid` activation with `1` neuron as this is a binary classification problem.

__2. Were you able to achieve the target model performance?__

The model was able to achieve `75.7%`, slightly above the required `75%`.

__3. What steps did you take in your attempts to increase model performance?__
> For reference, the baseline accuracy is `72.8%`.

- Data cleaning:
    - __Iteration 1__: Converted the `SPECIAL_CONSIDERATIONS` column to binary integers (`0`/`1`), instead of binary strings (`N`/`Y`).
    - __Iteration 2__: Accounted for missing category in the `INCOME_AMT` column.
        - __Iteration 2a__: Converting the `INCOME_AMT` column to ordinal encoding and retaining the original column results in a reduction of performance.
        - __Iteration 2b__: Dropping the `INCOME_AMT` column results in return to the baseline accuracy.
        - __Iteration 2c__: Creating `LOWER_INCOME` and `UPPER_INCOME` columns results in no change in accuracy, with a caveat of creating an "upper limit" for `50M+` as `100M`.
        - __Iteration 2d__: Take the average of the `LOWER_INCOME` and `UPPER_INCOME` columns to eliminate the pseudo upper limit created for `50M+`. Without dropping columns, the performance drops by 2%. However, dropping these intermediary columns (as well as `INCOME_AMT`) results in a return to the baseline accuracy.

- Feature Engineering:
    - __Iteration 3__: Created a new feature which compares the ask amount to the average income.
        - __Iteration 3a__: Initially, there was a reduction in performance, however experimented with comparing against `LOWER_INCOME` and returning the previously dropped `LOWER_INCOME` and `INCOME_AMT` columns, which resulted in a return to baseline accuracy. It seemed logical to only drop the `UPPER_INCOME` column, as there was synthetic data added to that column.
        - __Iteration 3b__: Experimented with retaining the `UPPER_INCOME` column as well, which resulted in only a slight decrease in accuracy. Will retain the column as it was used to calculate the `AVG_INCOME` anyway.
    - __Iteration 4__: Created new column by combining `AFFILIATION` with `ORGANIZATION`. This resulted in 73.6% accuracy, still close to the baseline but highest result so far.
    - __Iteration 5__: Created another column by combining `AFFILIATION` with `USE_CASE`.
    - __Iteration 6__: Added the `NAME` column back to the feature array, reduced to a maximum of 10 unique values to prevent a blowout when one-hot encoding. This resulted in the model achieving 75% accuracy.

- Hyperparameter Tuning:
    - Changed the number of epochs, to as low as `20` up to `200`.
    - Changed the kinds of activation functions. As the number of activation functions made available to the hidden layers is increased, the number of tuning trials also increased. Hence, there needed to be a tradeoff.
        - Avoided `linear` as did not want to introduce linearity to the model.
        - Avoided `sigmoid` in the hidden layers, as it would quash the value.
    - Changed the maximum number of neurons. Ultimately settled with a rule of thumb: "The number of hidden neurons should be less than twice the size of the input layer."

- Regularization:
    - Experimented with L1 (Lasso) and L2 (Ridge) regularizations.
    - L1 performed slightly better than L2, achieving the final `75.7%` compared to `74.8%`.

- Other Pre-Processing (iterations not saved):
    - Experimented with the number of unique values prior to encoding.
        - Maintained a maximum of `10` unique values, trialling values to as low as `6`.
        - Runs were also conducted with different values for different columns (i.e. `APPLICATION_TYPE` with `10` and `CLASSIFICATION` with `8`).
        - No improvements in performance was observed, although it was noted the performance decreases as more columns are removed.
    - Experimented with adding `EIN` back to the feature array, however no change in accuracy. This was removed again since there's no logical reason to use it as a feature.


## Summary
The initial model achieved an accuracy of `72.8%`, with the final model achieving an accuracy of `75.7%`. This is an improvement of `2.9%`, which is significant as the model struggled to achieve greater than `74%` on most runs, even after feature engineering and hyperparameter tuning. Although this is reasonable performance, it would be interesting to explore other models to achieve greater accuracy.

|![initial_run_accuracy](https://github.com/alyssahondrade/deep-learning-challenge/blob/main/images/initial_run_accuracy.png)|![initial_model_archi](https://github.com/alyssahondrade/deep-learning-challenge/blob/main/images/initial_model_architecture.png)|
|:---:|:---:|
|Initial Run|Initial Model Architecture|

|![final_run_accuracy](https://github.com/alyssahondrade/deep-learning-challenge/blob/main/images/final_run_accuracy.png)|![final_model_archi](https://github.com/alyssahondrade/deep-learning-challenge/blob/main/images/final_model_architecture.png)|
|:---:|:---:|
|Final Run|Final Model Architecture|

## Alternative Solutions
I would be interested to use ensemble learning to solve the same problem. My initial thought would be to use a Gradient Boosted Tree, given the small number of features available, however, I would need to be careful with overfitting. Otherwise, a Random Forest could also be used, applicable for smaller datasets but more robustness to overfitting. Regardless, the machine learning pipeline would still be applicable: data preprocessing, feature engineering, data splitting, model training, tuning, and evaluation, as demonstrated in the analysis.
