# AWS lambda function infrastructure
This project provides the required AWS resources to deploy an AWS lambda function.

## Prerequisites
- The [Terraform CLI (1.0.1+)](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started) installed.
- An [AWS Account](https://aws.amazon.com/free/)

## How to run
- Provide your AWS credentials
  ```
  export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
  export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
  ```
  _Make sure the user has the enough permissions to create all the resources listed in resources.tf._
- Initialize the configuration. 
  ```
  terraform init
  ```
- Apply the configuration. 🚀
  ```
  terraform apply
  ```
  If everything was good, you will get an output similar to this:
  ```
  Apply complete! Resources: 13 added, 0 changed, 0 destroyed.

  Outputs:
    base_url = "https://abcdef0j.execute-api.us-east-1.amazonaws.com/serverless_lambda_stage"
    function_name = "HelloWorld"
    lambda_bucket_name = "juanultimate-lightly-finally-brave-caribou"

  ```
  
## Troubleshooting
If you get an error like this:
```
╷
│ Error: Error creating S3 bucket: AccessDenied: Access Denied
│ 	status code: 403, request id: 6AYNH133YN6YSYH2, host id: Je2lZ1ceKDqxDZjUq321GzoY+FXDRB0uuRaddAExample=
│
│   with aws_s3_bucket.lambda_bucket,
│   on main.tf line 31, in resource "aws_s3_bucket" "lambda_bucket":
│   31: resource "aws_s3_bucket" "lambda_bucket" {
│
╵
╷
│ Error: Error creating IAM Role serverless_lambda: AccessDenied: User: arn:aws:iam::129900831382:user/terraform-client is not authorized to perform: iam:CreateRole on resource: arn:aws:iam::129900831382:role/serverless_lambda
│ 	status code: 403, request id: 8e905153-4912-441f-bffd-61ce2a42e51a
│
│   with aws_iam_role.lambda_exec,
│   on main.tf line 74, in resource "aws_iam_role" "lambda_exec":
│   74: resource "aws_iam_role" "lambda_exec" {
│
╵
╷
│ Error: error creating API Gateway v2 API: AccessDeniedException: User: arn:aws:iam::129900831382:user/terraform-client is not authorized to perform: apigateway:POST on resource: arn:aws:apigateway:us-east-1::/apis
│
│   with aws_apigatewayv2_api.lambda,
│   on main.tf line 96, in resource "aws_apigatewayv2_api" "lambda":
│   96: resource "aws_apigatewayv2_api" "lambda" {
│
╵
```
It means your user does not have the enough permission to create the required resources.