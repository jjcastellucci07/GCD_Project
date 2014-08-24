GCD_Project
===========

Project for Getting and Cleaning Data, part of the Data Science specialization


The script begins by downloading and unzipping the raw data from the web. The user is informed as each step of this process is completed, and is finally informed that the analysis has begun.

The script then writes functions that it will later use to extract and consolidate the data. The raw data is split into two groups and are stored in an atypical CSV format; these functions read the CSVs and merge the corresponding data into a single dataset.

The script then reads in and merges the subject, activity, and features data.  Appropriate column names are assigned and 



# Read in subject and activity columns
tidy_data <- rcon(2)
names(tidy_data) <- "Subject"
data <- rcon(4)
names(data) <- "Activity"
tidy_data <- cbind(tidy_data, data)

# Read in measurement data and assign appropiate column headers
data <- rcon (3)
feat <- read("./UCI HAR Dataset/features.txt")
names(data) <- as(feat[,2], "character")

# Extract only the mean and standard deviation columns for each measurement
for (i in 1:ncol(data)) {
  if(grepl("-mean()", names(data[i]), fixed = TRUE) | grepl("-std()", names(data[i]), fixed = TRUE)) {
    tidy_data <- cbind(tidy_data, data[i])
  }
}

data <- tidy_data
tidy_data <- data.frame()

# Calcuate the average of each variable for each activity and each subject.
for (i in 1:30) {
  for (j in 1:6) {
    splice <- data.frame(i,j)
    for (k in 3:68){
      splice <- cbind(splice,mean(data[data$Subject == i & data$Activity == j,k]))
    }
    tidy_data <- rbind(tidy_data, splice)
  }
}
names(tidy_data) <- names(data)

# Assign descriptive activity values
act <- read("./UCI HAR Dataset/activity_labels.txt")
for (i in 1:nrow(tidy_data)) {tidy_data[i,2] <- as(act[tidy_data[i,2], 2], "character")}

# Write tidy data to "HAR Tidy Dataset.txt"
print("Analysis complete. Writing results to file 'HAR Tidy Dataset.txt'")
write.table(tidy_data, file = "HAR Tidy Dataset.txt", row.names = F)