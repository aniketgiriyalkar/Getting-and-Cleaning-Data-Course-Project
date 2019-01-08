# Introduction

The script `run_analysis.R`performs the 5 steps described in the course project's definition.

* First, all the similar data is merged using the `rbind()` function. By similar, we address those files having the same number of columns and referring to the same entities.
* Then, only those columns with the mean and standard deviation measures are taken from the whole dataset. After extracting these columns, they are given the correct names, taken from `features.txt`.
* As activity data is addressed with values 1:6, we take the activity names and IDs from `activity_labels.txt` and they are substituted in the dataset.
* On the whole dataset, those columns with vague column names are corrected.
* Finally, we generate a new dataset with all the average measures for each subject and activity type (30 subjects * 6 activities = 180 rows). The output file is called `averages_data.txt`, and uploaded to this repository.

# Variables

* `x_train`, `y_train`, `x_test`, `y_test`, `subject_train` and `subject_test` contain the data from the downloaded files.
* `x_data`, `y_data` and `subject_data` merge the previous datasets to further analysis.
* `features` contains the correct names for the `x_data` dataset, which are applied to the column names stored in `mean_and_std_features`, a numeric vector used to extract the desired data.
* A similar approach is taken with activity names through the `activities` variable.
* `all_data` merges `x_data`, `y_data` and `subject_data` in a big dataset.
* Finally, `averages_data` contains the relevant averages which will be later stored in a `.txt` file. `ddply()` from the plyr package is used to apply `colMeans()` and ease the development.

# DETAILED INFORMATION ABOUT DATA

The dataset contains 180 observations and 81 variables.
Each observation is a combination of subject (30 volunteers) and activity (6 types) during which data was collected.



# VARIABLES EXPLANATION

1.  Activity - 6 values coded into WALKING (1), WALKING_UPSTAIRS (2), WALKING_DOWNSTAIRS (3), SITTING (4), STANDING (5), LAYING(6)
2.  Subject - 30 values representing observed volunteers

79 measure variables which are mean values from original normalized and bounded within [-1,1] features:

3.	tBodyAcc.mean.X
4.	tBodyAcc.mean.Y
5.	tBodyAcc.mean.Z
6.	tBodyAcc.std.X
7.	tBodyAcc.std.Y
8.	tBodyAcc.std.Z
9.	tGravityAcc.mean.X
10.	tGravityAcc.mean.Y
11.	tGravityAcc.mean.Z
12.	tGravityAcc.std.X
13.	tGravityAcc.std.Y
14.	tGravityAcc.std.Z
15.	tBodyAccJerk.mean.X
16.	tBodyAccJerk.mean.Y
17.	tBodyAccJerk.mean.Z
18.	tBodyAccJerk.std.X
19.	tBodyAccJerk.std.Y
20.	tBodyAccJerk.std.Z
21.	tBodyGyro.mean.X
22.	tBodyGyro.mean.Y
23.	tBodyGyro.mean.Z
24.	tBodyGyro.std.X
25.	tBodyGyro.std.Y
26.	tBodyGyro.std.Z
27.	tBodyGyroJerk.mean.X
28.	tBodyGyroJerk.mean.Y
29.	tBodyGyroJerk.mean.Z
30.	tBodyGyroJerk.std.X
31.	tBodyGyroJerk.std.Y
32.	tBodyGyroJerk.std.Z
33.	tBodyAccMag.mean
34.	tBodyAccMag.std
35.	tGravityAccMag.mean
36.	tGravityAccMag.std
37.	tBodyAccJerkMag.mean
38.	tBodyAccJerkMag.std
39.	tBodyGyroMag.mean
40.	tBodyGyroMag.std
41.	tBodyGyroJerkMag.mean
42.	tBodyGyroJerkMag.std
43.	fBodyAcc.mean.X
44.	fBodyAcc.mean.Y
45.	fBodyAcc.mean.Z
46.	fBodyAcc.std.X
47.	fBodyAcc.std.Y
48.	fBodyAcc.std.Z
49.	fBodyAcc.meanFreq.X
50.	fBodyAcc.meanFreq.Y
51.	fBodyAcc.meanFreq.Z
52.	fBodyAccJerk.mean.X
53.	fBodyAccJerk.mean.Y
54.	fBodyAccJerk.mean.Z
55.	fBodyAccJerk.std.X
56.	fBodyAccJerk.std.Y
57.	fBodyAccJerk.std.Z
58.	fBodyAccJerk.meanFreq.X
59.	fBodyAccJerk.meanFreq.Y
60.	fBodyAccJerk.meanFreq.Z
61.	fBodyGyro.mean.X
62.	fBodyGyro.mean.Y
63.	fBodyGyro.mean.Z
64.	fBodyGyro.std.X
65.	fBodyGyro.std.Y
66.	fBodyGyro.std.Z
67.	fBodyGyro.meanFreq.X
68.	fBodyGyro.meanFreq.Y
69.	fBodyGyro.meanFreq.Z
70.	fBodyAccMag.mean
71.	fBodyAccMag.std
72.	fBodyAccMag.meanFreq
73.	fBodyBodyAccJerkMag.mean
74.	fBodyBodyAccJerkMag.std
75.	fBodyBodyAccJerkMag.meanFreq
76.	fBodyBodyGyroMag.mean
77.	fBodyBodyGyroMag.std
78.	fBodyBodyGyroMag.meanFreq
79.	fBodyBodyGyroJerkMag.mean
80.	fBodyBodyGyroJerkMag.std
81.	fBodyBodyGyroJerkMag.meanFreq


(all information about measured features below comes from original features_info file which can be found here:
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones)

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals - tAcc-XYZ and tGyro-XYZ.
These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz.
Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise.
Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ)
using another low pass Butterworth filter with a corner frequency of 0.3 Hz.

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals
(tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated
using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag).

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing
fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag.
(Note the 'f' to indicate frequency domain signals).

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

The set of variables that were estimated from these signals are:

mean - Mean value

std - Standard deviation
