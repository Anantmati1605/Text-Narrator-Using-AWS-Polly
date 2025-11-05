# Text-Narrator-Using-AWS-Polly

## Project Description:
The text narrator project using AWS services i.e AWS Lambda, S3 Bucket, IAM, Amazon Polly to convert text files such as blog posts, articles, newsletters, or book excerpts into speech. It enables users to listen to articles, notes, or any custom text content, making information more accessible and engaging for visually impaired users, language learners, and multitaskers.

---

##  Architecture:

The system is built entirely on AWS serverless services:

- AWS Lambda – Serverless function that processes text and calls Amazon Polly.
- Amazon Polly – Text-to-Speech service that generates high-quality speech.
- Amazon S3 – Storage for uploaded .txt files and generated .mp3 files.
- IAM – Manages permissions for Lambda to access Polly and S3.

[Architecture Diagram]

<img width="1217" height="565" alt="Image" src="https://github.com/user-attachments/assets/3f824c45-3cd3-4b43-945f-23aedc57674f" />

---

##  Setup Instructions:
* Step 1: Create two S3 Buckets one is Source Bucket to upload .txt file and other is Destination Bucket to get store .mp3 audio file
* Step 2:  Create an IAM Policy to access polly and s3 bucket
  
  ```bash
  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:PutObject"
            ],
            "Resource": [
                "arn:aws:s3:::amzn-polly-bucket/*",
              "arn:aws:s3:::amzn-polly-destination-bucket/*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "polly:SynthesizeSpeech"
            ],
            "Resource": "*"
        }
    ]
  }

* Step 3: Create an IAM Role and attach above policy along with AWSLambdaBasicExecutionRole Policie
* Step 4: Create and Configure the Lambda Function. \
         - Set the execution role with necessary permissions for S3 and Polly. \
         - Add Environment Variables (`SOURCE_BUCKET`: Name of the source S3 bucket and `DESTINATION_BUCKET`: Name of the destination S3 bucket.)
* Step 5: Configure S3 Event Notification. \
         - Set up an event notification in the source S3 bucket to trigger the Lambda function on new object creation events with the `.txt` suffix.
* Step 6: Write Lambda Function Code (In repository .py file)
* Step 7: Upload .txt File in S3 Source Bucket then .mp3 audio file will be stored automatically in Destination Bucket.
* [AWSCloud.mp3](https://github.com/user-attachments/files/23358038/AWSCloud.mp3)

## Acknowledgments
This project was inspired by a course from [Yeshwanth L M](https://github.com/yeshwanthlm). 




 
