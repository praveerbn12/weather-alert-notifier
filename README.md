# Weather Alert Notifier

An AWS serverless weather alert system that allows users to receive weather-based notifications using cloud-native services.

## Live Demo

http://weather-alert-ist615.s3-website-us-east-1.amazonaws.com/

## Project Overview

Weather Alert Notifier is a cloud-based application designed to monitor weather conditions and notify users when specific weather thresholds are met.

The project was built as part of a cloud computing course to demonstrate a serverless architecture using AWS services such as Lambda, EventBridge, DynamoDB, SNS, API Gateway, and S3.

## Problem

Users often need timely weather alerts for conditions such as high temperature, rain, storms, or other weather changes. A traditional always-running server can be costly and unnecessary for this type of scheduled alert system.

## Solution

This project uses a serverless and event-driven AWS architecture. A scheduled EventBridge rule triggers a Lambda function, which checks weather data from an external weather API, compares it against stored user preferences, and sends alerts using Amazon SNS.

## Tech Stack

- AWS Lambda
- Amazon EventBridge
- Amazon DynamoDB
- Amazon SNS
- Amazon API Gateway
- Amazon S3
- OpenWeatherMap API
- HTML/CSS/JavaScript

## Architecture

```text
User
 ↓
S3 Static Website
 ↓
API Gateway
 ↓
Lambda
 ↓
DynamoDB

EventBridge Schedule
 ↓
Lambda Weather Check
 ↓
OpenWeatherMap API
 ↓
Threshold Evaluation
 ↓
SNS Notification
```

## AWS Services Used

### Amazon S3
Used to host the static frontend website.

### Amazon API Gateway
Used to expose backend endpoints for user registration or alert configuration.

### AWS Lambda
Used to run backend logic without managing servers.

### Amazon EventBridge
Used to trigger scheduled weather checks.

### Amazon DynamoDB
Used to store user email addresses and weather alert preferences.

### Amazon SNS
Used to send weather alert notifications to users.

## Key Features

- Static web dashboard hosted on S3
- Serverless backend using AWS Lambda
- Scheduled weather checks using EventBridge
- User preference storage using DynamoDB
- Email/SMS-style alerting using SNS
- External weather data integration using OpenWeatherMap API

## Why Serverless?

This project does not require a continuously running server. Serverless architecture is a good fit because weather checks happen on a schedule and backend logic runs only when triggered.

Benefits:

- Lower operational overhead
- Cost-efficient for scheduled workloads
- Easy scaling
- No server maintenance
- Event-driven design

## Learning Outcomes

This project helped me understand:

- Serverless application design
- Event-driven cloud architecture
- AWS Lambda triggers
- DynamoDB usage for lightweight configuration storage
- SNS-based notification workflows
- Static website hosting using S3
- How multiple AWS services work together in a real application

## Future Improvements

- Add authentication for users
- Add support for multiple cities
- Add dashboard history for previous alerts
- Add CloudWatch logs and monitoring screenshots
- Add Terraform or CloudFormation for infrastructure as code
- Improve frontend UI and validation

## Status

The live static website is deployed on Amazon S3. Additional source code, screenshots, and architecture documentation will be added as future improvements.
