# Project: Data Modeling with Postgres

## Introduction
A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project. Your role is to create a database schema and ETL pipeline for this analysis. You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.

## Datasets
### Song Dataset
The first dataset is a subset of real data from the [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong/). Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.

> song_data/A/B/C/TRABCEI128F424C983.json
> song_data/A/A/B/TRAABJL12903CDCF1A.json

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

`{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}`

## Log Dataset

The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate activity logs from a music streaming app based on specified configurations.

The log files in the dataset you'll be working with are partitioned by year and month. For example, here are filepaths to two files in this dataset.

> log_data/2018/11/2018-11-12-events.json
> log_data/2018/11/2018-11-13-events.json

And below is an example of what the data in a log file, 2018-11-12-events.json, looks like.

![log file data example](https://video.udacity-data.com/topher/2019/February/5c6c15e9_log-data/log-data.png)

## Schema for Song Play Analysis
The start schema optimized for song play analysis includes the following tables:
### Fact Table
1. songplays - records in log data associated with song plays i.e. records with page NextSong
 - songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
 
### Dimension Tables
2. users - users in the app
 - user_id, first_name, last_name, gender, level
3. songs - songs in music database
 - song_id, title, artist_id, year, duration
4. artists - artists in music database
 - artist_id, name, location, latitude, longitude
5. time - timestamps of records in songplays broken down into specific units
 - start_time, hour, day, week, month, year, weekday

## Project files
The project includes six files:
1. test.ipynb displays the first few rows of each table to check the database.
2. create_tables.py drops and creates the tables. Run this file to reset tables before each time run the ETL scripts.
3. etl.ipynb reads and processes a single file from song_data and log_data and loads the data into the tables. This notebook contains detailed instructions on the ETL process for each of the tables.
4. etl.py reads and processes files from song_data and log_data and loads them into the tables. This is based on my work in the ETL notebook.
5. sql_queries.py contains all the sql queries, and is imported into the last three files above.
6. README.md provides discription and discussion of the project.

## Project Steps

### Create Tables
1. Write CREATE statements in sql_queries.py to create each table.
2. Write DROP statements in sql_queries.py to drop each table if it exists.
3. Run create_tables.py to create the database and tables.
4. Run test.ipynb to confirm the creation of your tables with the correct columns. Make sure to click "Restart kernel" to close the connection to the database after running this notebook.

### Build ETL Processes
In the `etl.ipynb` notebook to develop ETL processes for each table. At the end of each table section, or at the end of the notebook, run `test.ipynb` to confirm that records were successfully inserted into each table. Remember to rerun `create_tables.py` to reset your tables before each time you run this notebook.

### Build ETL Pipeline
Use what have been completed in `etl.ipynb` to complete etl.py, where the entire datasets will be processed. Remember to run `create_tables.py` before running `etl.py` to reset your tables. Run `test.ipynb` to confirm the records were successfully inserted into each table.

## Project Results
### Fact Table - songplays (records in log data associated with song plays i.e. records with page NextSong)
![Fact Table - songplays](/tables_screenshot/Songplays_table_screenshot.JPG "Fact Table - songplays")

### Dimension Tables
#### users - users in the app
![Dimension Table - users](/tables_screenshot/Users_table_screenshot.JPG "Dimension Table - users")

#### songs - songs in music database
![Dimension Table - songs](/tables_screenshot/songs_table_screenshot.JPG "Dimension Table - songs")

#### artists - artists in music database
![Dimension Table - artists](/tables_screenshot/artists_table_screenshot.JPG "Dimension Table - artists")

#### time - timestamps of records in songplays broken down into specific units
![Dimension Table - time](/tables_screenshot/time_table_screenshot.JPG "Dimension Table - time")

