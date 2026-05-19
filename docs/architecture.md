# Weather Alert Notifier Architecture

## Architecture Overview

Weather Alert Notifier uses an AWS serverless architecture to check weather conditions on a schedule and notify users when their selected alert thresholds are met.

The system is designed to avoid always-running servers. Instead, backend logic runs only when triggered by user actions or scheduled events.

## High-Level Flow

```text
User
 ↓
S3 Static Website
 ↓
API Gateway
 ↓
Lambda Registration Function
 ↓
DynamoDB


EventBridge Scheduled Rule
 ↓
Lambda Weather Checker
 ↓
OpenWeatherMap API
 ↓
Threshold Evaluation
 ↓
SNS Notification
 ↓
User Email Alert
```

## Component Breakdown

## 1. Amazon S3

Amazon S3 hosts the static frontend website.

The frontend allows users to interact with the application through a browser without requiring a traditional web server.

## 2. Amazon API Gateway

API Gateway provides HTTP endpoints for the frontend.

It acts as the entry point between the static website and backend Lambda functions.

## 3. AWS Lambda

Lambda handles backend logic.

Main Lambda responsibilities:

- Receive user alert configuration
- Store user preferences in DynamoDB
- Fetch weather data from OpenWeatherMap
- Compare current weather conditions with user thresholds
- Trigger SNS alerts when conditions match

## 4. Amazon DynamoDB

DynamoDB stores user alert preferences.

Example stored data:

```text
email
city
temperature_threshold
weather_condition
alert_enabled
```

## 5. Amazon EventBridge

EventBridge triggers the weather-checking Lambda function on a schedule.

Example:

```text
Run every 15 minutes
```

This makes the system event-driven instead of requiring a continuously running backend server.

## 6. OpenWeatherMap API

The Lambda function calls OpenWeatherMap to retrieve current weather data for the selected city.

## 7. Amazon SNS

SNS sends weather alert notifications to users.

When a weather condition meets the stored threshold, Lambda publishes a message to an SNS topic.

## Why This Architecture?

This architecture is a good fit because weather alerts are event-based and scheduled. There is no need to keep a server running 24/7.

Benefits:

- Serverless
- Cost-efficient
- Scalable
- Low maintenance
- Event-driven
- Easy to extend

## Future Architecture Improvements

- Add user authentication with Amazon Cognito
- Add infrastructure as code using Terraform or CloudFormation
- Add CloudWatch dashboards for monitoring
- Store alert history in DynamoDB
- Add support for multiple alert types
- Add retry and error-handling logic for failed weather API calls
