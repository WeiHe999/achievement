## avm_report step function pipeline:

* The pipeline aims to store the evaluation data, new sales, new listing for a specified month into Postgres database.

* The pipeline is scheduled to be run at 00:00 on the 20th of every month, triggered by cloud watch.

* To run the pipeline manually, use the input as below (the year_month need to be changed to the right year_month):
{
  "year_month": "2021-12",
  "bucket": "rnd-avm-v2-dev"
}

## avm_report dashboard server

* set up an EC2 instance at AWS, allow access to TCP port 8501 in security group setting

* Install python packages: psycopg2-binary, plotly_express, streamlit, sqlalchemy

* Run the server in a tmux terminal: streamlit run avm_report.py



