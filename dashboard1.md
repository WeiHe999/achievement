# oak_level_dashboard_v1

## How to create an oak_level_dashboard dev version?

* Create a git branch from master branch

* Change the variable **experiment_version** in main.tf

* Change the Python script **server.py** based on experiment needs

* Run **terraform apply** to deploy the EC2 server

* SSH to the server and then start the server by running **start_server.sh** in dashboard folder

* Access the dashboard via: http://private_ip_address:8501/
