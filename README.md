

# Summary
* Get Guardduty dumb data from AWS S3
* Iterate over the data
* Filter data base on severity
* Extract only the the relevant data

# API AutoFlow Version:
Configuration config.json was created using AutoFlow version __0.2.5__

# Need help?
Is you have questions about this example, feel free to post your question on the community "<a href="https://www.interactor.com/support/forum" target="_blank">Ask Questions</a>" website.

# Data extraction

## Flow overview
1. HTTP Server
2. Endpoint (Method: GET)
3. Action __communication/http-request__ to make the HTTP API call to AWS S3
4. Action __json/decode__ to make the JSON easier to use
5. Action __data/set__ to create an empty array for storing the extracted database
6. Action __iteration/for-each__ to iterate over the Guard Duty data which is in array
7. Action __condition/match__ to filter only the data that matches certain condition
8. Action __array/insert-at__ to insert the extracted data into the array
9. Action __data/set__ to set the result in the response body
![Image](https://github.com/API-AutoFlow/api-data-extraction/blob/master/img/1.png)

## Step 1. Make HTTP API Call to Guard Duty
Enter the AWS S3 bucket. Sample Guard Duty data provided below
https://autoflow-files.s3-us-west-2.amazonaws.com/guardduty+data.json
The returned data is stored in a new variable called "result"

![Image](https://github.com/API-AutoFlow/api-data-extraction/blob/master/img/2.png)

## Step 2. Decode JSON data
Guard Duty returns the data in JSON format.  We can use the json/decode action to put the data in a more accessible format.

![Image](https://github.com/API-AutoFlow/api-data-extraction/blob/master/img/3.png)

## Step 3. Create (declare) empty array
Array is commonly used to structure extracted data. Before we iterate over the Guard Duty data, we use data set to delcare/create an empty array.

![Image](https://github.com/API-AutoFlow/api-data-extraction/blob/master/img/4.png)

## Step 4. Iterate over Guard Duty data
Notice that decoded Guard Duty data was saved in a variable called "result_decoded".
Each element's index and value are stored in index and value variables respectively.

![Image](https://github.com/API-AutoFlow/api-data-extraction/blob/master/img/5.png)

## Step 5. Filter data based on severity
Use the Match/condition action to select only the data that matches the condition. In our case, we are looking for the severity of the security incidents.

![Image](https://github.com/API-AutoFlow/api-data-extraction/blob/master/img/6.png)

## Step 6. Condition for the match
Match can have many conditions. In our case, the condition is severity greater than or equal to 2.

![Image](https://github.com/API-AutoFlow/api-data-extraction/blob/master/img/7.png)

## Step 5. Insert only the relevant data
As the Guard Duty data is iterated, array/insert-at action inserts the selected data into the "sorted" array that was created earlier

![Image](https://github.com/API-AutoFlow/api-data-extraction/blob/master/img/8.png)

## Step 6. Set data to response body
To make the data available, data/set action is used to set data in the response body.

![Image](https://github.com/API-AutoFlow/api-data-extraction/blob/master/img/9.png)
