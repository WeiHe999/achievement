# Experiment v20220203

## Description:
* Changes made in this experiment: 
```
# line 128 in avm_v2_5_prod_worker_knn
early_date2 = pd.to_datetime(target_sold_date)+relativedelta(
        months=-3) # change from 2 to 3
```
* Retrain the model using year-month 202110

## Training
* Step function input:
```
{
  "job_key": "Train20220203",
  "version": "v20220203",
  "year_month": 202110,
  "task": "training",
  "bucket": "rnd-avm-v2-dev"
}
```

## Evaluation:
* Step function input:
```
{
  "job_key": "EvProd20220203",
  "version": "v20220203",
  "year_month": 202110,
  "task": "batch_transform",
  "training_job_key": "Train20220203",
  "bucket": "rnd-avm-v2-dev",
  "test_data_key": "avm2.5/production/monthly-evaluation/v20220202/df_sales.csv"
}
```

* Test data: out-of-time test set with sales from 2021-10-01 to 2021-12-31.

* Evaluation notebook: https://dev-yifeng-2-large-node.notebook.ca-central-1.sagemaker.aws/notebooks/avm2.5/994-production-monthly-evaluation/2022-02/01_avmv2_5_evaluation_v20220203.ipynb

* Evaluation result: s3://rnd-avm-v2-dev/avm_v2_5_production_evaluation/202110/Train20220203/out-of-time-evaluation/df_Eval20220203.csv

| Metric        | Value         |
| ------------- |:-------------:|
| Test size     | 19234         |
| Median-APE    | 0.0921        |
| Mean-APE      | 0.2291        |
| Within-15%    | 0.6717        |

