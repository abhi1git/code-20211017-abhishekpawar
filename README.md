# code-20211017-abhishekpawar
## **SNS-SQS-Lambda CFT**

* This repository consists of Cloudformation templates to Setup SNS-SQS-Lambda-S3 architecture
* Nested Cloudformation Stack Approach is used here to implement Separation of Concerns
* SNS sends message notification to a specific Queue on the basis of Subscription Filter policy i.e If the message attribute has `event_type = important` then only the message is sent to the SQS Queue
* Once SQS receives the message it invokes the Lambda, as SQS event acts as a trigger to the Lambda in this setup
* Lambda extracts the Message body from the event stores it in a file and puts the file object to the specified S3 bucket
* SQS access policy is configured such as particular SQS can receive messages from specific SNS Topic
* Bucket Name is being passed as environment variable to the Lambda to avoid changes in code if destination bucket needs to be changed anytime
* Lambda Logs retention is set to 90 days
* Lifecycle Rules are configured on S3 bucket to move the data to Standard IA storage class after 30 days, move to Glacier after 90 days & delete after 365 days  
  
---
### **Deploying Cloudformation**
* Upload all files to a S3 bucket
* Copy the S3 URL of the `bootstrap.yaml` file and give it as an input to the Cloudformation service while creating the stack
* All the input parameters are assigned default values which can be changed in the AWS console
* After clicking on Create Stacks Cloudformation will create Nested Stacks

---  
## [Efficiency & Security Improvements](https://github.com/abhi1git/code-20211017-abhishekpawar/blob/main/NOTES.txt)

---
