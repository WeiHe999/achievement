# Experiment v20220202

## Description:
* No change from master branch
* Retrain the model using year-month 202110

## Training
* Step function input:
```
{
  "job_key": "Train20220202",
  "version": "v20220202",
  "year_month": 202110,
  "task": "training",
  "bucket": "rnd-avm-v2-dev"
}
```

## Evaluation:
* Step function input:
```
{
  "job_key": "EvProd20220202",
  "version": "v20220202",
  "year_month": 202110,
  "task": "batch_transform",
  "training_job_key": "Train20220202",
  "bucket": "rnd-avm-v2-dev",
  "test_data_key": "avm2.5/production/monthly-evaluation/v20220202/df_sales.csv"
}
```

* Test data: out-of-time test set with sales from 2021-10-01 to 2021-12-31.

* Evaluation notebook: https://dev-yifeng-2-large-node.notebook.ca-central-1.sagemaker.aws/notebooks/avm2.5/994-production-monthly-evaluation/2022-02/01_avmv2_5_evaluation_v20220202.ipynb

* Evaluation result:


| Left columns  | Right columns |
| ------------- |:-------------:|
| left foo      | right foo     |
| left bar      | right bar     |
| left baz      | right baz     |


| Metric        | Value         |
| ------------- |:-------------:|
| Test size     | right foo     |
| Median_APE    | right bar     |
| Mean_APE      | right baz     |
| Within_15%    | right baz     |




