# Alphabet Soup Analysis

## Table of Contents
1. [Goal]()
2. [Questions]()
    1. [Data Preprocessing]()
    2. [Compiling, Training, and Evaluating the Model]()
3. [Summary]()


## Goal
Explain the purpose of the analysis


The purpose of the analysis is...

## Questions
Answer all 6 questions in the results section

### Data Preprocessing
1. What variable(s) are the target(s) for your model?

2. What variable(s) are the features for your model?

3. What variable(s) should be removed from the input data because they are neither targets nor features?


### Compiling, Training, and Evaluating the Model
1. How many neurons, layers, and activation functions did you select for your neural network model, and why?

2. Were you able to achieve the target model performance?

3. What steps did you take in your attempts to increase model performance?
- Data cleaning:
    - (Iteration 1) Converted the `SPECIAL_CONSIDERATIONS` column to binary integers (`0`/`1`), instead of binary strings (`N`/`Y`).
    - (Iteration 2) Accounted for missing category in the `INCOME_AMT` column.
    - Added the `NAME` column back to the feature array, reduced to a maximum of 10 unique values to prevent a blowout when one-hot encoding.
    
__STEPS THAT DID NOT WORK__
- Added `EIN` back to the feature array. No change in accuracy. Removed it again since no logical reason to use it as a feature.
- Converting the `INCOME_AMT` column to ordinal encoding and retaining the original column results in a reduction of performance. Dropping the `INCOME_AMT` column results in return to the baseline accuracy.

## Summary
Format images in the report so that they display correction
Summarise the overall results of your model
|![img_name]()|
|:---:|
|image_title|

## Alternative Solutions
Describe how you could use a different model to solve the same problem, and explain why you would use that model