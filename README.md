# Lacrosse-game-stream

## Summary
This project centers around constructing a dynamic data processing pipeline tailored for a simulated lacrosse game stream. Key objectives encompass real-time box score generation during live gameplay and the subsequent updating of player and team statistics within a database post-game.

## Technologies / Tools Used:
-  **Apache Spark**: Employed for data processing, ETL, and analysis.
-  **Docker**: The project environment is set up using Docker containers managed by Docker Compose.
-  **MinIO**: An S3-compatible object store that holds the live game stream data.
-  **Microsoft SQL Server**: A database for storing player and team reference data.
-  **MongoDB**: A NoSQL database for storing real-time box score data post-transformation for website development.
-  ***Apache Drill**: A SQL query engine for data exploration.

## Data Dictionary and Data Sources
-  **Game Stream** _(minio/gamestreams/gamestream.txt)_:
  This file comprises events from a simulated lacrosse game, featuring a unique event ID, timestamp, team and player identifiers, and indicating whether the event resulted in a goal.

- **Player and Team Reference Data** _(mssql)_:
The player and team reference data is stored in the Microsoft SQL Server, with the following tables:
  - **teams table**: Stores team information, including team ID, name, conference, wins, and losses.
  - **players table**: Stores player information, including player ID, name, jersey number, shots, goals, and team ID.

## Setup


## ETL Pipeline
The project follows an ETL (Extract, Transform, Load) pipeline to process the lacrosse game data and update the reference data. The pipeline consists of the following stages:

### Extract
The extraction stage involves reading data from the following sources:

-  **Game Stream Data**: Extracts game stream data from minio/gamestreams/gamestream.txt in MinIO object storage. This file contains a simulated stream of events during a lacrosse game.
-  **Player and Team Reference Data**: Extract player and team reference data from MS-SQL Server on Microsoft SQL Server. This data includes player names, jersey numbers, shots, goals, and team information.

### Transform
In the transformation stage, the extracted data undergoes several operations:
-  **Game Stream Processing**: Processes the game stream data to calculate player and team statistics based on events during the game, aggregating shots taken, goals scored, and updating team scores.
-  **Data Joining**: Joins the processed game stream data with player and team reference data to create a comprehensive dataset, including in-game statistics and reference information.
-  **Box Score Formatting**: Transforms the joined data into the desired box score format, including team names, scores, player names, player statistics (shots, goals, shooting percentage), and the current game status (winning, losing, or tied).

### Load
The load stage involves writing transformed data to appropriate destinations:
-  **Real-time Box Score Data**: During the game, the transformed box score data into MongoDB/boxscores collection in MongoDB. This collection stores real-time box score data in JSON format, consumable by web developers for display on a website.
-  **Updated Reference Data**: After the game, create two new tables (players2 and teams2) in mssql database on Microsoft SQL Server. These tables contain updated player and team reference data, reflecting changes in statistics and records based on the game outcome.

## Conclusion:
In conclusion, this project delivers a robust and flexible data processing pipeline tailored for lacrosse game data.
