# CODEBOOK

This Codebook describes my two datasets and the original dataset from which it was derived. This is entitled entitled "Human Activity Recognition Using Smartphones Data Set" and is abstracted as "Human Activity Recognition database built from the recordings of 30 subjects performing activities of daily living (ADL) while carrying a waist-mounted smartphone with embedded inertial sensors".  

A full description with links to the entire dataset can be found here:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

## Citation Request:

[1] Davide Anguita, Alessandro Ghio, Luca Oneto, Xavier Parra and Jorge L. Reyes-Ortiz. Human Activity Recognition on Smartphones using a Multiclass Hardware-Friendly Support Vector Machine. International Workshop of Ambient Assisted Living (IWAAL 2012). Vitoria-Gasteiz, Spain. Dec 2012


## Original Data Set Information:

The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain. 

## Attribute Information:

For each record in the dataset it is provided: 
- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration. 
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.




## DATASET 1 - SELECTED OBSERVATIONS 
##    (MEANS ands STANDARD DEVIATIONS)

My first data set combined the original dataset test and train data and took a subset of only those variables associated with a mean or standard deviation. Combined with descriptive columns for Activity and Subject I produced a dataset of 69  variables over 10,299 rows.

ActivityLabel is an integer referencing the 6 activities described by ActivityDescription.
Subject is an integer identifying each of the 30 subjects.
The variables names can be identified as time or frequency by the names first letter. These differ from the originals in that they have been tidied to remove extraneous characters "(" and ")" and have had hyphens replaced with underscores. The terms "mean" and "std" were replaced with "Mean" and "StDv" for readability.

- ActivityLabel             
- ActivityDescription       
- Subject                   
- tBodyAcc_Mean_X           
- tBodyAcc_Mean_Y           
- tBodyAcc_Mean_Z           
- tGravityAcc_Mean_X        
- tGravityAcc_Mean_Y        
- tGravityAcc_Mean_Z        
- tBodyAccJerk_Mean_X       
- tBodyAccJerk_Mean_Y       
- tBodyAccJerk_Mean_Z       
- tBodyGyro_Mean_X          
- tBodyGyro_Mean_Y          
- tBodyGyro_Mean_Z          
- tBodyGyroJerk_Mean_X      
- tBodyGyroJerk_Mean_Y      
- tBodyGyroJerk_Mean_Z      
- tBodyAccMag_Mean          
- tGravityAccMag_Mean       
- tBodyAccJerkMag_Mean      
- tBodyGyroMag_Mean         
- tBodyGyroJerkMag_Mean     
- fBodyAcc_Mean_X           
- fBodyAcc_Mean_Y           
- fBodyAcc_Mean_Z           
- fBodyAccJerk_Mean_X       
- fBodyAccJerk_Mean_Y       
- fBodyAccJerk_Mean_Z       
- fBodyGyro_Mean_X          
- fBodyGyro_Mean_Y          
- fBodyGyro_Mean_Z          
- fBodyAccMag_Mean          
- fBodyBodyAccJerkMag_Mean  
- fBodyBodyGyroMag_Mean     
- fBodyBodyGyroJerkMag_Mean 
- tBodyAcc_StDv_X           
- tBodyAcc_StDv_Y           
- tBodyAcc_StDv_Z           
- tGravityAcc_StDv_X        
- tGravityAcc_StDv_Y        
- tGravityAcc_StDv_Z        
- tBodyAccJerk_StDv_X       
- tBodyAccJerk_StDv_Y       
- tBodyAccJerk_StDv_Z       
- tBodyGyro_StDv_X          
- tBodyGyro_StDv_Y          
- tBodyGyro_StDv_Z          
- tBodyGyroJerk_StDv_X      
- tBodyGyroJerk_StDv_Y      
- tBodyGyroJerk_StDv_Z      
- tBodyAccMag_StDv          
- tGravityAccMag_StDv       
- tBodyAccJerkMag_StDv      
- tBodyGyroMag_StDv         
- tBodyGyroJerkMag_StDv     
- fBodyAcc_StDv_X           
- fBodyAcc_StDv_Y           
- fBodyAcc_StDv_Z           
- fBodyAccJerk_StDv_X       
- fBodyAccJerk_StDv_Y       
- fBodyAccJerk_StDv_Z       
- fBodyGyro_StDv_X          
- fBodyGyro_StDv_Y          
- fBodyGyro_StDv_Z          
- fBodyAccMag_StDv          
- fBodyBodyAccJerkMag_StDv  
- fBodyBodyGyroMag_StDv     
- fBodyBodyGyroJerkMag_StDv 


## DATASET 2 - DATASET 1 AVERAGED BY SUBJECT WITHIN ACTIVITY

This summary file aggregates Dataset 1 by Activity and Subject to provide a mean for each group.Names are as for Dataset 1 but with the addition of "_average" where appropriate to signify the summarising.

- ActivityLabel                        
- ActivityDescription                  
- Subject                              
- tBodyAcc_Mean_X_average              
- tBodyAcc_Mean_Y_average              
- tBodyAcc_Mean_Z_average              
- tGravityAcc_Mean_X_average           
- tGravityAcc_Mean_Y_average           
- tGravityAcc_Mean_Z_average           
- tBodyAccJerk_Mean_X_average          
- tBodyAccJerk_Mean_Y_average          
- tBodyAccJerk_Mean_Z_average          
- tBodyGyro_Mean_X_average             
- tBodyGyro_Mean_Y_average             
- tBodyGyro_Mean_Z_average             
- tBodyGyroJerk_Mean_X_average         
- tBodyGyroJerk_Mean_Y_average         
- tBodyGyroJerk_Mean_Z_average         
- tBodyAccMag_Mean_average             
- tGravityAccMag_Mean_average          
- tBodyAccJerkMag_Mean_average         
- tBodyGyroMag_Mean_average            
- tBodyGyroJerkMag_Mean_average        
- fBodyAcc_Mean_X_average              
- fBodyAcc_Mean_Y_average              
- fBodyAcc_Mean_Z_average              
- fBodyAccJerk_Mean_X_average          
- fBodyAccJerk_Mean_Y_average          
- fBodyAccJerk_Mean_Z_average          
- fBodyGyro_Mean_X_average             
- fBodyGyro_Mean_Y_average             
- fBodyGyro_Mean_Z_average             
- fBodyAccMag_Mean_average             
- fBodyBodyAccJerkMag_Mean_average     
- fBodyBodyGyroMag_Mean_average        
- fBodyBodyGyroJerkMag_Mean_average    
- tBodyAcc_StDv_X_average              
- tBodyAcc_StDv_Y_average              
- tBodyAcc_StDv_Z_average              
- tGravityAcc_StDv_X_average           
- tGravityAcc_StDv_Y_average           
- tGravityAcc_StDv_Z_average           
- tBodyAccJerk_StDv_X_average          
- tBodyAccJerk_StDv_Y_average          
- tBodyAccJerk_StDv_Z_average          
- tBodyGyro_StDv_X_average             
- tBodyGyro_StDv_Y_average             
- tBodyGyro_StDv_Z_average             
- tBodyGyroJerk_StDv_X_average         
- tBodyGyroJerk_StDv_Y_average         
- tBodyGyroJerk_StDv_Z_average         
- tBodyAccMag_StDv_average             
- tGravityAccMag_StDv_average          
- tBodyAccJerkMag_StDv_average         
- tBodyGyroMag_StDv_average            
- tBodyGyroJerkMag_StDv_average        
- fBodyAcc_StDv_X_average              
- fBodyAcc_StDv_Y_average              
- fBodyAcc_StDv_Z_average              
- fBodyAccJerk_StDv_X_average          
- fBodyAccJerk_StDv_Y_average          
- fBodyAccJerk_StDv_Z_average          
- fBodyGyro_StDv_X_average             
- fBodyGyro_StDv_Y_average             
- fBodyGyro_StDv_Z_average             
- fBodyAccMag_StDv_average             
- fBodyBodyAccJerkMag_StDv_average     
- fBodyBodyGyroMag_StDv_average        
- fBodyBodyGyroJerkMag_StDv_average    

