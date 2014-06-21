# README


########################################################################################################
# Initialise
########################################################################################################

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

########################################################################################################
# Add names to the columns of the 3 combined tables
########################################################################################################

names(all) <- c("ActivityLabel", "Subject", xcolheaders)

########################################################################################################
# Remove any value columns that are not either a mean or a standard deviation
########################################################################################################

colnames <- names(all)
collabel <- colnames[1:2] # save ActivityLabel, Subject
colmeans <- grep("_Mean", colnames, value = TRUE) # all Mean columns
colstdev <- grep("_StDv", colnames, value = TRUE) # all Standard Deviation columns
keepcolnames <- c(collabel, colmeans, colstdev) # create list of columns to keep
all <- all[ , keepcolnames] # subset based on columns to keep
all <- merge(activitylabels, all)   # Add a column for Activity Description

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

########################################################################################################
# End
########################################################################################################
