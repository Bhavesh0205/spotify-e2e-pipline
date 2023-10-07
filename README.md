# Spotify End-to-End Pipeline

### Introduction
The goal is to build an ETL pipeline using the Spotify API on AWS. The pipeline will rerieve data from Spotify API, transform it to a desired format and load it into AWS data store.

### ETL Process Overview
1. Extract
-Extract data from Spotify API using the Spotipy library
-Deploy the data extraction code using the Lambda function
-Run trigger using EventBridge to automate data extraction every Tuesday at 6 pm
-Data extract is saved in the spotify-etl-project-bhavesh/raw_data/to_process folder in the S3 bucket

2. Transform
-Run S3 trigger when any new data is added into the spotify-etl-project-bhavesh/raw_data/to_process folder in the S3 bucket. This will run the data transformation code on Lambda
-The transformation code will clean and transform the data to prepare 3 files for the album, artist, and songs. The data will be stored in the 3 subfolders in transformed_data. Lastly, files in the to_process folder will be copied to the processed folder and files in to_process will be deleted. We are just moving data from one folder to another.

3. Load
-Glue crawler will infer schema when new data arrives in the 3 folders in the transformed_data folder
-Data catalog manage metadata repository
-Query S3 data using Athena

