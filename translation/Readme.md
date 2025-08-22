Translation API Project
Overview
This project implements a simple Translation API using AWS Lambda and Amazon Translate. The API accepts text input and a target language, translates the text using AWS Translate, and returns the translated result. It is deployed via AWS API Gateway for easy access and testing.
Features

Translates text into a specified language using AWS Translate.
Supports automatic source language detection.
Default target language is Spanish (es), but can be customized.
Error handling for missing input or service issues.
Deployed as a serverless application with API Gateway integration.

Prerequisites

AWS Account with access to:
AWS Lambda
AWS Translate
AWS API Gateway
IAM for role creation


Python 3.x installed locally for development and testing.
AWS CLI configured with appropriate credentials.
Basic understanding of AWS services and Python.

Installation

Clone the Repository:
git clone <repository-url>
cd translation-api


Set Up AWS Credentials:

Configure AWS CLI with your credentials:aws configure


Ensure you have permissions to create Lambda functions, IAM roles, and API Gateway resources.


Install Dependencies:

The project uses the boto3 library, which is included in the AWS Lambda environment. No additional installation is needed for deployment.


Deploy the Lambda Function:

Package the lambda_function.py file and deploy it to AWS Lambda using the AWS CLI or console.
Attach the required IAM role with permissions for AWS Translate and CloudWatch Logs.


Configure API Gateway:

Create a new API in API Gateway.
Define a POST /translate route and integrate it with the Lambda function.
Deploy the API to the $default stage.



Usage
API Endpoint
The API is accessible at the deployed URL, e.g.:
https://<api-id>.execute-api.us-east-1.amazonaws.com/default/translate

Request Example
Send a POST request with a JSON body:
curl -X POST "https://<api-id>.execute-api.us-east-1.amazonaws.com/default/translate" \
-H "Content-Type: application/json" \
-d "{\"text\": \"Guten Tag Welt\", \"target\": \"en\"}"

Response Example
{
  "statusCode": 200,
  "body": "{\"translatedText\": \"Good day world\"}"
}

Error Handling

Missing Text: Returns 400 with {"error": "Missing \"text\" in request"}.
Internal Error: Returns 500 with {"error": "<error_message>"}.

Configuration

IAM Role: The Lambda function requires an IAM role with:
translate:TranslateText permission.
logs:CreateLogGroup, logs:CreateLogStream, and logs:PutLogEvents for CloudWatch logging.


Environment Variables: No environment variables are currently used, but can be added for configuration (e.g., default target language).

Development

Code: Edit lambda_function.py to modify the translation logic or add features.
Testing: Test locally with a Python environment or use the AWS Lambda console with a test event:{
  "body": "{\"text\": \"Hello world\", \"target\": \"es\"}"
}


Deployment: Update the Lambda function and redeploy the API Gateway stage after changes.

Contributing

Fork the repository.
Create a new branch (git checkout -b feature-branch).
Make changes and commit (git commit -m "Add new feature").
Push to the branch (git push origin feature-branch).
Open a pull request.

License
This project is licensed under the MIT License - see the LICENSE file for details.
Contact
For questions or support, contact the project maintainer at [your-email@example.com].
