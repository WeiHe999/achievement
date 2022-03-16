# edm_condo_v2

## edm_condo_v2 models

### Description

* Trained with Zillow ground-truth data, KNN table is edm_condo_v2.knn_base 
* edm_condo_v2 training job names:
```
{'numberofbaths':       'edm-TrainCatA1V3-numberofbat01',
 'foundationtype':      'edm-TrainCatA1V3-foundationt01',
 'finishedbasement':    'edm-TrainCatA1V3-finishedbas01',
 'rooftype':            'edm-TrainCatA1-rooftype-31',
 'numberofstoreys':     'edm-TrainB5-numberofstoreys-17',
 'exteriorwalltype':    'edm-TrainB5-exteriorwalltype17',
 'garagetype':          'edm-TrainA6-garagetype-44',
 'architecturalstyle':  'edm-TrainA6-architecturalsty44',
 'yearbuilt':           'edm-TrainNumA1-yearbuilt-41',
 'totalfloorarea':      'edm-TrainNumA1-totalfloorare41'}
```
* edm_condo_v2 step-function training job-keys:
```
{'numberofbaths':      'TrainCatA1V3',
 'foundationtype':     'TrainCatA1V3',
 'finishedbasement':   'TrainCatA1V3',
 'rooftype':           'TrainCatA1',
 'numberofstoreys':    'TrainB5',
 'exteriorwalltype':   'TrainB5',
 'garagetype':         'TrainA6',
 'architecturalstyle': 'TrainA6',
 'yearbuilt':          'TrainNumA1',
 'totalfloorarea':     'TrainNumA1'}
```
* edm_condo_v2 models are used to score national datalake
* URL for edm_condo_v2 model dict:
```
s3://rnd-sagemaker-model-artifacts-dev/model_dict/edm_condo_v2/dict_config.pickle
```

### Re-train:
* Step function inputs:
``` 
{
  "job_key": "TrainCatK1",
  "task": "training",
  "targets": "numberofbaths, foundationtype, finishedbasement, rooftype",
  "bucket": "rnd-edm-v4-dev"
}
{
  "job_key": "TrainNumK1",
  "task": "training",
  "targets": "yearbuilt, totalfloorarea",
  "bucket": "rnd-edm-v4-dev"
}
{
  "job_key": "TrainCatK2",
  "task": "training",
  "targets": "numberofstoreys, exteriorwalltype, architecturalstyle, garagetype",
  "bucket": "rnd-edm-v4-dev"
}
```

### Batch transform for test set evaluation or datalake scoring:
* Step function inputs:
```
# Test set evaluation
{
  "job_key": "EvalTrainCatA1V3PV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "numberofbaths, foundationtype, finishedbasement",
  "task": "batch_transform",
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainCatA1V3"
}
{
  "job_key": "EvalTrainCatA1PV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "rooftype",
  "task": "batch_transform",
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainCatA1"
}
{
  "job_key": "EvalTrainB5PV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "numberofstoreys, exteriorwalltype",
  "task": "batch_transform",
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainB5"
}
{
  "job_key": "EvalTrainA6PV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "garagetype, architecturalstyle",
  "task": "batch_transform",
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainA6"
}
{
  "job_key": "EvalTrainNumA1PV",
  "test_data_key": "evaluation/pv/df_test.csv",
  "targets": "yearbuilt, totalfloorarea",
  "task": "batch_transform",
  "bucket": "rnd-edm-v4-dev",
  "training_job_key": "TrainNumA1"
}
```
* For datalake scoring, set **test_data_key** to: datalake/data/df_1.csv, datalake/data/df_2.csv, datalake/data/df_3.csv, datalake/data/df_4.csv, datalake/data/df_5.csv, respectively.

### Base data:
* Step function input:
```
{
  "job_key": "Base202202",
  "task": "base_data",
  "bucket": "rnd-edm-v4-dev"
}
```
