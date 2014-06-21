# README



## Overview

The assignment requires that I access a dataset entitled "Human Activity Recognition Using Smartphones Data Set" and perform various operations to extract, filter, transform, tidy and describe it. A full description of the original datset can be found at http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones and I have  added the README from the original daatset at the bottom of this document as a reference.

## The Task

My task involves creating an R script called run_analysis.R that does the following:

1. Merges the training and the test sets to create one data set.
- Extracts only the measurements on the mean and standard deviation for each measurement. 
- Uses descriptive activity names to name the activities in the data set
- Appropriately labels the data set with descriptive variable names. 
- Creates a second, independent tidy data set with the average of each variable for each activity and each subject. 

I have addressed these steps as follows.

## Step 0 - Initialisation

This is a pre-requisite to the stated 5 steps.  Here I set up my working directory, initialise required libraries and read in the files that describe the columns and rows of the primary dataset.

As part of this step I also tidy the column names by removing and replacing characters ("()" removed, hyphens replaced with underscores, mean to Mean and std to StDv)
```
library(plyr)
projectdir <- "F:/DATA/MOO/DataCleaning/Ass/"
setwd(projectdir)

########################################################################################################
# Obtain Labels and corresponding Descriptions
########################################################################################################

# change to the unzipped data directory
setwd("./data/UCI HAR Dataset")

# load the activity labels and descriptions
activitylabels <- read.table("activity_labels.txt")
names(activitylabels) <- c("ActivityLabel","ActivityDescription")

# load the feature descriptions to be used as column headers
features <- read.table("features.txt")
xcolheaders <- as.character(features[,2])

# tidy up the column headers to be used
# Remove the (), replace hyphens with underscores, format the type (Mean or StDv)
xcolheaders <- gsub("-mean\\(\\)", "_Mean", xcolheaders)
xcolheaders <- gsub("-std\\(\\)", "_StDv", xcolheaders)
xcolheaders <- gsub("-", "_", xcolheaders)

```

## Step 1 - Merge

The 3 test and 3 train files were read to tables and the rows combined for each of the 3 pairs.

The three resultant tables were then combined with descriptive rows preceding variable rows.

```
########################################################################################################
# Load the test and train data 
########################################################################################################

subjecttest <- read.table("./test/subject_test.txt")
xtest <- read.table("./test/X_test.txt")
ytest <- read.table("./test/y_test.txt")

subjecttrain <- read.table("./train/subject_train.txt")
xtrain <- read.table("./train/X_train.txt")
ytrain <- read.table("./train/y_train.txt")

########################################################################################################
# Combine the rows for the 3 sets each of test and train tables
########################################################################################################

subject <- rbind(subjecttest,subjecttrain)
x <- rbind(xtest, xtrain)
y <- rbind(ytest, ytrain)

########################################################################################################
# Combine the columns of the 3 tables
########################################################################################################

all <- cbind(subject, x)
all <- cbind(y, all)

```

## Step 2 - Extract mean and Standard deviation

Based on the standardised columns names those with _Mean or _StDv were extracted

```
########################################################################################################
# Remove any value columns that are not either a mean or a standard deviation
########################################################################################################

colnames <- names(all)
collabel <- colnames[1:2] # save ActivityLabel, Subject
colmeans <- grep("_Mean", colnames, value = TRUE) # all Mean columns
colstdev <- grep("_StDv", colnames, value = TRUE) # all Standard Deviation columns
keepcolnames <- c(collabel, colmeans, colstdev) # create list of columns to keep
all <- all[ , keepcolnames] # subset based on columns to keep

```

## Step 3 - Activity Descriptions added

Using "merge" the ActivityDescriptions were added

```
all <- merge(activitylabels, all)   # Add a column for Activity Description
```

## Step 4 - Appropriate labelling

This was done in both the initialisation process as described above and with the addition "_average" in the resulting "TidyData" summary file.

```
names(allsummary) <- paste(names(allsummary), "_average", sep="") # add "average" to column names
```

## Step 5 - Tidy Data file

Produced with the aggregate function and verified as in the correct order (ie Activity then Subject)

```

########################################################################################################
# Get the means by Activity, Subject; update the column names and add a the activity description
########################################################################################################

allsummary <- aggregate(all[c(colmeans, colstdev)], by = list(all$Subject, all$ActivityLabel), mean)
names(allsummary) <- paste(names(allsummary), "_average", sep="") # add "average" to column names
colnames(allsummary)[1:2] <- c("Subject", "ActivityLabel") # restore the col names for the grouped columns
allsummary <- merge(activitylabels, allsummary)   # Add a column for Activity Description

# note that the aggregation was done in Subject, Activity order to create the appropriate row order
# the columns were then ordered correctly by the merge - there is probably a more elegant way to do it

########################################################################################################
# Write the tidy data file
########################################################################################################

setwd(projectdir)
write.table(allsummary, "tidydata.txt", row.names = FALSE )
```


# README from the original dataset

## Human Activity Recognition Using Smartphones Dataset

## Version 1.0

Jorge L. Reyes-Ortiz, Davide Anguita, Alessandro Ghio, Luca Oneto.
Smartlab - Non Linear Complex Systems Laboratory
DITEN - Università degli Studi di Genova.
Via Opera Pia 11A, I-16145, Genoa, Italy.
activityrecognition@smartlab.ws
www.smartlab.ws


The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain. See 'features_info.txt' for more details. 

## For each record it is provided:


- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.

## The dataset includes the following files:


- 'README.txt'

- 'features_info.txt': Shows information about the variables used on the feature vector.

- 'features.txt': List of all features.

- 'activity_labels.txt': Links the class labels with their activity name.

- 'train/X_train.txt': Training set.

- 'train/y_train.txt': Training labels.

- 'test/X_test.txt': Test set.

- 'test/y_test.txt': Test labels.

## The following files are available for the train and test data. Their descriptions are equivalent. 

- 'train/subject_train.txt': Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30. 

- 'train/Inertial Signals/total_acc_x_train.txt': The acceleration signal from the smartphone accelerometer X axis in standard gravity units 'g'. Every row shows a 128 element vector. The same description applies for the 'total_acc_x_train.txt' and 'total_acc_z_train.txt' files for the Y and Z axis. 

- 'train/Inertial Signals/body_acc_x_train.txt': The body acceleration signal obtained by subtracting the gravity from the total acceleration. 

- 'train/Inertial Signals/body_gyro_x_train.txt': The angular velocity vector measured by the gyroscope for each window sample. The units are radians/second. 

## Notes: 

- Features are normalized and bounded within [-1,1].
- Each feature vector is a row on the text file.

For more information about this dataset contact: activityrecognition@smartlab.ws

## License:

Use of this dataset in publications must be acknowledged by referencing the following publication [1] 

[1] Davide Anguita, Alessandro Ghio, Luca Oneto, Xavier Parra and Jorge L. Reyes-Ortiz. Human Activity Recognition on Smartphones using a Multiclass Hardware-Friendly Support Vector Machine. International Workshop of Ambient Assisted Living (IWAAL 2012). Vitoria-Gasteiz, Spain. Dec 2012

This dataset is distributed AS-IS and no responsibility implied or explicit can be addressed to the authors or their institutions for its use or misuse. Any commercial use is prohibited.

Jorge L. Reyes-Ortiz, Alessandro Ghio, Luca Oneto, Davide Anguita. November 2012.
