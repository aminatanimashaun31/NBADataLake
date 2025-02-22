## NBADataLake
This repository contains the setup_nba_data_lake.py script, which automates the creation of a data lake for NBA analytics using AWS services. The script integrates Amazon S3, AWS Glue, and Amazon Athena, and sets up the infrastructure needed to store and query NBA-related data.

## Overview
The setup_nba_data_lake.py script performs the following actions:

Creates an Amazon S3 bucket to store raw and processed data. Uploads sample NBA data (JSON format) to the S3 bucket. Creates an AWS Glue database and an external table for querying the data. Configures Amazon Athena for querying data stored in the S3 bucket.

## Prerequisites
Before running the script, ensure you have the following:

Go to Sportsdata.io and create a free account At the top left, you should see "Developers", if you hover over it you should see "API Resources" Click on "Introduction & Testing"

Click on "SportsDataIO API Free Trial" and fill out the information & be sure to select NBA for this tutorial

You will get an email and at the bottom it says "Launch Developer Portal"

By default it takes you to the NFL, on the left click on NBA

Scroll down until you see "Standings"

You'll "Query String Parameters", the value in the drop down box is your API key.

Copy this string because you will need to paste it later in the script

IAM Role/Permissions: Ensure the user or role running the script has the following permissions:

S3: s3:CreateBucket, s3:PutObject, s3:DeleteBucket, s3:ListBucket Glue: glue:CreateDatabase, glue:CreateTable, glue:DeleteDatabase, glue:DeleteTable Athena: athena:StartQueryExecution, athena:GetQueryResults

## START HERE
Step 1: Open CloudShell Console
Go to aws.amazon.com & sign into your account

In the top, next to the search bar you will see a square with a >_ inside, click this to open the CloudShell

Step 2: Create the setup_nba_data_lake.py file
In the CLI (Command Line Interface), type
nano setup_nba_data_lake.py
In another window, go to GitHub
-Copy the contents inside the setup_nba_data_lake.py file

-Go back to the Cloudshell window and paste the contents inside the file.

Find the line of code under #Sportsdata.io configurations that says "api_key" paste your api key inside the quotations

Press ^X to exit, press Y to save the file, press enter to confirm the file name

Step 3: Create .env file
In the CLI (Command Line Interface), type
nano .env
paste the following line of code into your file, ensure you swap out with your API key
SPORTS_DATA_API_KEY=your_sportsdata_api_key
NBA_ENDPOINT=https://api.sportsdata.io/v3/nba/scores/json/Players
Press ^X to exit, press Y to save the file, press enter to confirm the file name
Step 4: Run the script
In the CLI type
python3 setup_nba_data_lake.py
-You should see the resources were successfully created, the sample data was uploaded successfully and the Data Lake Setup Completed
![image](https://github.com/user-attachments/assets/9de9952e-7a2e-4949-be9b-cf5683b6f47f)


Step 5: Manually Check For The Resources
In the Search Bar, type S3 and click blue hyper link name
-You should see 2 General purpose bucket named "Sports-analytics-data-lake"


-When you click the bucket name you will see 3 objects are in the bucket

Click on raw-data and you will see it contains "nba_player_data.json"

Click the file name and at the top you will see the option to Open the file

-You'll see a long string of various NBA data
![image](https://github.com/user-attachments/assets/5add67cf-04b6-4721-9441-8cb6a00b58c1)
![image](https://github.com/user-attachments/assets/b0f5dfd4-8d6c-46f3-8b7a-bf25665138c0)
![image](https://github.com/user-attachments/assets/a6976a20-1281-411a-a27d-c588f15bc905)
![image](https://github.com/user-attachments/assets/c3e60837-72ed-4a76-bcd1-d6e844fd2def)



Head over to Amazon Athena and you could paste the following sample query:
![image](https://github.com/user-attachments/assets/2ab17021-a673-45ef-9ad0-b639a7feef13)

![image](https://github.com/user-attachments/assets/8c677fa3-2571-403f-a202-398883f076d3)

![image](https://github.com/user-attachments/assets/908bd554-aacd-40f8-b04e-863325768889)




SELECT FirstName, LastName, Position, Team
FROM nba_players
WHERE Position = 'PG';
-Click Run -You should see an output if you scroll down under "Query Results"

![image](https://github.com/user-attachments/assets/98b45536-0341-4549-a22a-2843111694ac)
![image](https://github.com/user-attachments/assets/60a83cdf-975b-4794-8eb5-7b6d04cccdf9)

![image](https://github.com/user-attachments/assets/95dba0a6-0d39-4b36-873c-f8c855bcc4f7)





## What I Learned
Securing AWS services with least privilege IAM policies.
Automating the creation of services with a script.
Integrating external APIs into cloud-based workflows.
Future Enhancements
Automate data ingestion with AWS Lambda
Implement a data transformation layer with AWS Glue ETL
Add advanced analytics and visualizations (AWS QuickSight)
