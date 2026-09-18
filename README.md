# Predicting Maintenance Labor Hours for University Work Orders

**B104C Artificial Intelligence & Machine Learning — Individual Project**

## Project question

Can information available when a maintenance work order starts help estimate its required labor effort accurately enough to support a university's workload planning?

I use the Facility Management Unified Classification Database (FMUCD), version 1, and focus on work orders from University 1. After cleaning, 118,406 records remain. The predictors describe the building, work priority, start month, system and subsystem. I assume these fields can be recorded at work-order start. Labor hours are the target. I exclude information such as final work-order duration and cost because it would not be available when the estimate is needed.

## Methods and findings

I use a fixed 60/20/20 training, validation and test split. I compare median and mean baselines with linear regression and K-nearest-neighbours (KNN), and test PCA and a log-transformed target. Models and settings are selected from validation results before assessment on the separate test set. K-means is used separately to explore whether work orders form useful groups.

The selected model is KNN with two neighbours, a log-transformed target and no PCA. Its test MAE is 2.845 hours, compared with 3.366 hours for the median baseline. However, the overall result hides an important weakness. For jobs requiring more than eight labor hours, the model has an MAE of 25.04 hours and underestimates 94.9% of jobs. The K-means groups also have weak separation. I therefore would not use the current results to allocate workers automatically. I would first test the estimates alongside a planner's judgement on newly recorded work orders.

The conclusions apply to the filtered records from one university and to a random split of similar work orders. They do not demonstrate performance on unfamiliar buildings, other universities or future years.

## Main files

- [Jupyter notebook](B104C_AI_and_ML_Assignment.ipynb) contains the complete analysis, results and references.
- [Data instructions](data/README.md) explain how to obtain and place the source CSV.
- [Python requirements](requirements.txt) lists the packages needed to rerun the analysis.

## Running the notebook

I used Python 3.12. The dependencies are listed in [requirements.txt](requirements.txt) and can be installed with `pip install -r requirements.txt`. Place the source CSV in `data/` as described below and run the notebook from the project folder.

## Dataset

The source is FMUCD version 1 by Pampana et al. (2024), available from [Mendeley Data](https://data.mendeley.com/datasets/cb8d2nsjss/1) under CC BY 4.0. The 1.44 GB CSV is excluded from Git. To run a cloned copy, download the dataset and place it in the `data` folder as described in [data/README.md](data/README.md).
