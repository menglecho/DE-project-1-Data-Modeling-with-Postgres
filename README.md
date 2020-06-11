# DE-project-1-Data-Modeling-with-Postgres

Project: Data Modeling with Postgres

-Introduction
	A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

	They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project. Your role is to create a database schema and ETL pipeline for this analysis. You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.

- Project Description
	In this project, you'll apply what you've learned on data modeling with Postgres and build an ETL pipeline using Python. To complete the project, you will need to define fact and dimension tables for a star schema for a particular analytic focus, and write an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.

- Schema for Song Play Analysis 
	Using the song and log datasets, you'll need to create a star schema optimized for queries on song play analysis. This includes the following tables.

- Fact Table 
	songplays records in log data associated with song plays i.e. records with page NextSong songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

- Dimension Tables 
	users - users in the app user_id, first_name, last_name, gender, level 
	songs - songs in music database song_id, title, artist_id, year, duration 
	artists - artists in music database artist_id, name, location, latitude, longitude 
	time - timestamps of records in songplays broken down into specific units start_time, hour, day, week, month, year, weekday

- How it works:
	Implementing a star schema with songplays at its centre as a fact table, with as its dimensions: songs, users, artists and time.

	sql_queries.py: containts the SQL queries to create the tables, to insert rows and a SELECT query to find song_id and artist_id based on the song name, artist name and song length.

	create_tables.py: connects to the database and builds a sparkify database if doesn't exists. Once the database is created, this fils executes the SQL queries in sql_queries.py to build tables in the schema.

	etl.py: processes the JSON files containing song, artist, user and songplay data into the tables. It also uses pandas library to perform some aspects of the ETL

	etl.ipynb: implements the same script as etl.py, but on a single song file and log file.

	test.ipynb: contains a number of SQL query to test the contents of the various tables after the ETL has been performed

- How to use the scripts:
	To build the schema(or to drop the tables and rebuild them)
	python create_tables.py

	To execute the ETL to load data into the tables
	python etl.py

	Some queries used to test the results of the ETL using test.ipynb:

	%sql SELECT name, title FROM songs NATURAL JOIN artists LIMIT 5;

	%sql SELECT * FROM songplays JOIN songs ON songplays.song_id = songs.song_id
		JOIN artists ON songplays.artist_id = artists.artist_id
		JOIN time ON songplays.start_time = time.start_time
		JOIN users ON songplays.user_id = users.user_id
		LIMIT 5;

	%sql SELECT * FROM songplays WHERE song_id != 'None' LIMIT 5;
