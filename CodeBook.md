CODEBOOK for Getting and cleaning data course project

The original code for this project was taken from 
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

A copy is also available in the git repository

the Following files were used in creating the new data set for this analysis. These already had the mean calculations were were interested in. 

X_test.txt X_train.txt > the data recorded by the devices, 

y_test.txt y_train.txt > An index representing the activity for every observation in the X data 

subject_train.txt and subject_test.txt > containing the subject number of the 30 people in the experiment. There’s a subject id for every observation in the X data set

activity_labels.txt >  has the index of the activity number by activity name

features.txt > has the list of names for the 561 variables


To assemble the data from the raw files for the analysis the following rational was used

1) As the 3 training files and the 3 testing data files had the same number of rows respectively. It made sense to deal with these separately and then add them together

The training files were combined using cbind to produce a data frame with the following columns (not named at this stage)

subject | activity index | data (561) columns

The same was done with the data from test files 

2) The training data was then added to the test data using rbind


3) Next column names were added to the merged data table as follows

First column was named ‘subjectid’ 
Second column was named ‘activity’ 
All subsequent columns were named using the corresponding variable names provided in features.txt

4) Having combined all the data,as per task 2 in the project, the variables containing just the mean and standard deviations were selected. For this exercise only variable names containing mean() or std() were included such as tBodyAcc-min()-X. Other variables where the mean or std appeared in the middle or without the () such as angle(X,gravityMean) were excluded as it was clear from the info that these were relevant. 



5) The activity number was substituted with the name of the activity corresponding to the activity_labels.txt provided in the test file

6) Next to tidy the data - the parenthesis () and hyphens were removed from the columns names

7) All column names were changed to lower case

8) For the last task in the assignment of summarising the means for each variable by the activity and subject

- The data was grouped first by ‘activity’ then by ‘subject’
- Then the summarise_each was used to calculate the mean for each variable by the two groups

9) Finally the new data table was written to the file tidy-data.txt


*********** Variable names

For each activity and by subject the mean is was calculated for the following variables
tbodyaccmeanxtbodyaccmeanytbodyaccmeanztbodyaccstdxtbodyaccstdytbodyaccstdztgravityaccmeanxtgravityaccmeanytgravityaccmeanztgravityaccstdxtgravityaccstdytgravityaccstdztbodyaccjerkmeanxtbodyaccjerkmeanytbodyaccjerkmeanztbodyaccjerkstdxtbodyaccjerkstdytbodyaccjerkstdztbodygyromeanxtbodygyromeanytbodygyromeanztbodygyrostdxtbodygyrostdytbodygyrostdztbodygyrojerkmeanxtbodygyrojerkmeanytbodygyrojerkmeanztbodygyrojerkstdxtbodygyrojerkstdytbodygyrojerkstdztbodyaccmagmeantbodyaccmagstdtgravityaccmagmeantgravityaccmagstdtbodyaccjerkmagmeantbodyaccjerkmagstdtbodygyromagmeantbodygyromagstdtbodygyrojerkmagmeantbodygyrojerkmagstdfbodyaccmeanxfbodyaccmeanyfbodyaccmeanzfbodyaccstdxfbodyaccstdyfbodyaccstdzfbodyaccjerkmeanxfbodyaccjerkmeanyfbodyaccjerkmeanzfbodyaccjerkstdxfbodyaccjerkstdyfbodyaccjerkstdzfbodygyromeanxfbodygyromeanyfbodygyromeanzfbodygyrostdxfbodygyrostdyfbodygyrostdzfbodyaccmagmeanfbodyaccmagstdfbodybodyaccjerkmagmeanfbodybodyaccjerkmagstdfbodybodygyromagmeanfbodybodygyromagstdfbodybodygyrojerkmagmeanfbodybodygyrojerkmagstd

