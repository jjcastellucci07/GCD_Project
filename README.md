GCD_Project
===========

Project for Getting and Cleaning Data, part of the Data Science specialization on Coursera.

# Preparation

The script begins by downloading and unzipping the raw data from the web. The user is informed as each step of this process is completed, and is finally informed that the analysis has begun.

The script then writes functions that it will later use to extract and consolidate the data. The raw data is split into two groups and are stored in an atypical CSV format; these functions read the CSVs and merge the corresponding data into a single dataset.

# Analysis

The script then reads in and merges the subject, activity, and features data.  Appropriate column names are assigned and features other than *mean* and *standard deviation* are removed. The average each remaining feature is then calculated and recorded for each combination of subject and activity. Finally, the activity values are changed from numbers to usful descriptions.

# Results

When the analysis is complete the user is notified and the results of the analysis are written to the working directory to a file named **HAR Tidy Dataset.txt**.