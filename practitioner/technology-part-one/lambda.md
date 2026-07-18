# Lambda

- This is the serverless feature offering by the aws that **run our code without having provision or manage servers
- Aws maintains scaling,capacity provsisioning and logging.

> **Note :** Serverless means its not there wont be any servers. If you want to run your code somewhere you definitly need server. SO AWS lambda what will do is is has **reserved service pool** so when event is triggered event means from other sources hit the code of your's which is in lambda means that time **lambda catch the event and it will find the instance which is reserved and run our code**

## Use cases

### 1. Image Processing

- Triggered when an image is uploaded to an S3 bucket.
- Automatically resizes or compresses images.
- Example: Generate profile picture thumbnails.

### 2. Send Emails

- Triggered after user registration or order confirmation.
- Sends welcome emails, OTPs, invoices, or notifications using Amazon SES.

### 3. File Processing

- Triggered when files are uploaded to S3.
- Reads CSV, Excel, or JSON files.
- Stores processed data into DynamoDB or RDS.

---
## Benefits of Lambda

- No server to manage
- No need for an infra team
- no pathcing/upgrading
- Faster development
- Autoscale to handle traffic spikes
- Pay for what you use

## Downside of lambda

- No local state we cant store the persist data
- Function can run at most for 15 minutes, after that i will close. Not good for long running tasks
- Cold starts issues occurs due to the time it takes t initialziw and load the functin. But Snapstart and provisoned concurrency helps cold starts issue

## Lambda Pricing

- Number of times function ran
- How long did it run for
- How much memory/cpu did it require


# How Lambda is Triggered

AWS Lambda is **event-driven**, meaning it runs only when an event occurs.

## Common Trigger Methods

### 1. Direct Invocation (AWS SDK)

- Backend directly invokes the Lambda function using the AWS SDK.
- Suitable when the application needs an immediate Lambda execution.

**Flow:**

```
React UI
    │
POST /register
    │
Spring Boot
    │
Save User
    │
Invoke Lambda
    │
Lambda
    │
Send Email (SES)
```

---
