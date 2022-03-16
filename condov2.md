# edm_condo_v2

## edm_condo_v2 models

### Description

* Trained with ground-truth data from **opta_data.construction_features_condo**, KNN table is **edm_condo_v2.knn_base** 
* edm_condo_v2 training job names:
```
{'totalfloorarea':       'T-TrainNum6A-totalfloorarea-22',
 'yearbuilt':            'T-ondo-TrainNum6A-yearbuilt-22',
 'numberofstoreys':      'T-rainNum6A-numberofstoreys-22',
 'floorlevel':           'T-ndo-TrainNum6A-floorlevel-22',
 'numberofbaths':        'T--TrainCat6A-numberofbaths-59',
 'numberofbedrooms':     'T-ainCat6A-numberofbedrooms-59',
 'numberofdens':         'T-o-TrainCat6A-numberofdens-59',
 'architecturalstyle':   'T-nCat6A-architecturalstyle-59'}
```
* edm_condo_v2 step-function training job-keys:
```
{'totalfloorarea':       'TrainNum6A',
 'yearbuilt':            'TrainNum6A',
 'numberofstoreys':      'TrainNum6A',
 'floorlevel':           'TrainNum6A',
 'numberofbaths':        'TrainCat6A',
 'numberofbedrooms':     'TrainCat6A',
 'numberofdens':         'TrainCat6A',
 'architecturalstyle':   'TrainCat6A'}
```
* edm_condo_v2 models are used to score national datalake
* URL for edm_condo_v2 model dict:
```
s3://rnd-sagemaker-model-artifacts-dev/model_dict/edmcondo_v2/dict_config.pickle
```

### Re-train:
* Step function inputs:
* "version" in step function input needs to be the same to the experiment_version defined in terraform script (variables.tf)
``` 
{
  "job_key": "TrainNum7A",
  "task": "training",
  "targets": "totalfloorarea, yearbuilt, numberofstoreys, floorlevel",
  "bucket": "rnd-edm-condo-v2-dev",
  "version": "v0"
}
{
  "job_key": "TrainCat7A",
  "task": "training",
  "targets": "numberofbaths, numberofbedrooms, numberofdens, architecturalstyle",
  "bucket": "rnd-edm-condo-v2-dev",
  "version": "v0"
}
```

### Batch transform for test set evaluation or datalake scoring:
* Step function inputs:
```
# Test set evaluation
{
  "job_key": "TestNum6AV2",
  "test_data_key": "base_data/TrainNum6A/result/df_test_set.csv",
  "targets": "totalfloorarea, yearbuilt, numberofstoreys, floorlevel",
  "task": "batch_transform",
  "version": "v0",
  "bucket": "rnd-edm-condo-v2-dev",
  "training_job_key": "TrainNum6A"
}
{
  "job_key": "TestCat6AV2",
  "test_data_key": "base_data/TrainCat6A/result/df_test_set.csv",
  "targets": "numberofbaths, numberofbedrooms, numberofdens, architecturalstyle",
  "task": "batch_transform",
  "version": "v0",
  "bucket": "rnd-edm-condo-v2-dev",
  "training_job_key": "TrainCat6A"
}
```
* For datalake scoring, set **test_data_key** to: datalake/data/df_1.csv, datalake/data/df_2.csv, datalake/data/df_3.csv, datalake/data/df_4.csv, datalake/data/df_5.csv, respectively.

### Base data:
* Step function input:
```
{
  "job_key": "Base202203",
  "task": "base_data",
  "bucket": "rnd-edm-condo-v2-dev",
}
```
