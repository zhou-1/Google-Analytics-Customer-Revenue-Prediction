# What files do I need?
You will need to download train_v2.csv and test_v2.csv. These contain the data necessary to make predictions for each fullVisitorId listed in sample_submission_v2.csv.

You can also access a subset of this data via BigQuery, using the example notebook provided as a way to get started. These subsets are contained in the BigQuery ga_train_set and ga_test_set datasets, under the kaggle-public-datasets project, accessible through Kernels. In those BigQuery datasets, each day's worth of data is a separate table for more efficient EDA / download.

All information below pertains to the data in both CSV and BigQuery format.

What should I expect the data format to be?
Both train_v2.csv and test_v2.csv contain the columns listed under Data Fields. Each row in the dataset is one visit to the store. Because we are predicting the log of the total revenue per user, be aware that not all rows in test_v2.csv will correspond to a row in the submission, but all unique fullVisitorIds will correspond to a row in the submission.

IMPORTANT: Due to the formatting of fullVisitorId you must load the Id's as strings in order for all Id's to be properly unique!
There are multiple columns which contain JSON blobs of varying depth. In one of those JSON columns, totals, the sub-column transactionRevenue contains the revenue information we are trying to predict. This sub-column exists only for the training data.

What am I predicting?
We are predicting the natural log of the sum of all transactions per user. Once the data is updated, as noted above, this will be for all users in test_v2.csv for December 1st, 2018 to January 31st, 2019. For every user in the test set, the target is:
yuser=∑i=1ntransactionuseri
targetuser=ln(yuser+1)
Note that the dataset does NOT contain data for December 1st 2018 to January 31st 2019. You must identify the unique fullVisitorIds in the provided test_v2.csv and make predictions for them for those unseen months.

File Descriptions
Note: These have not yet been updated, per the "Important Note" above.

train.csv - the old training set - contains the same data as the BigQuery rstudio_train_set. Contains user transactions from August 1st 2016 to August 1st 2017.
test.csv - the old test set - contains the same data as the BigQuery rstudio_test_set. Contains user transactions from August 2nd 2017 to April 30th 2018.
sampleSubmission.csv - the old sample submission file in the correct format. Contains all fullVisitorIds in test.csv.

train_v2.csv - the updated training set - contains user transactions from August 1st 2016 to April 30th 2018.

test_v2.csv - the updated test set - contains user transactions from May 1st 2018 to October 15th 2018.
sample_submission_v2.csv - a updated sample submission file in the correct format. Contains all fullVisitorIds in test_v2.csv. Your submission's PredictedLogRevenue column should make forward-looking predictions for each of these fullVisitorIds for the timeframe of December 1st 2018 to January 31st 2019. Review "What am I predicting?" above for details.
Data Fields
fullVisitorId- A unique identifier for each user of the Google Merchandise Store.
channelGrouping - The channel via which the user came to the Store.
date - The date on which the user visited the Store.
device - The specifications for the device used to access the Store.
geoNetwork - This section contains information about the geography of the user.
sessionId - A unique identifier for this visit to the store.
socialEngagementType - Engagement type, either "Socially Engaged" or "Not Socially Engaged".
totals - This section contains aggregate values across the session.
trafficSource - This section contains information about the Traffic Source from which the session originated.
visitId - An identifier for this session. This is part of the value usually stored as the _utmb cookie. This is only unique to the user. For a completely unique ID, you should use a combination of fullVisitorId and visitId.
visitNumber - The session number for this user. If this is the first session, then this is set to 1.
visitStartTime - The timestamp (expressed as POSIX time).
Removed Data Fields
Some fields were censored to remove target leakage. The major censored fields are listed below.

hits - This row and nested fields are populated for any and all types of hits. Provides a record of all page visits.
customDimensions - This section contains any user-level or session-level custom dimensions that are set for a session. This is a repeated field and has an entry for each dimension that is set.
totals - Multiple sub-columns were removed from the totals field.
External Data
External data is permitted for this competition, per this forum post. This includes the Google Merchandise Store Demo Account. Although the Demo Account contains the predicted variable, final standings will not benefit from access to this external data, because it requires future-looking predictions.
