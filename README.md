# AWS SNS integration with slack/teams channels

This pattern demonstrates how you can setup a fully serverless setup to integrate your SNS topic with Slack/Teams channel. This provisions AWS resources for you and you just need to integrate your Slack/Teams webhooks to get it running.

[Learn more about this pattern at Serverless Land Patterns](https://serverlessland.com/repos/sns-slack-teams-cloudFormation-python)

[SNS & Slack/Teams integration diagram](https://github.com/ajayv-AWS/Img/blob/870961eb05a4732ea2ee6a36af8ad1fd6a7ef206/SNS-teams-slack.drawio.png?raw=true)

Important: this application uses various AWS services and there are costs associated with these services after the Free Tier usage - please see the [AWS Pricing page](https://aws.amazon.com/pricing/) for details. You are responsible for any AWS costs incurred. No warranty is implied in this example.

## Requirements

* [Create an AWS account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) if you do not already have one and log in. The IAM user that you use must have sufficient permissions to make necessary AWS service calls and manage AWS resources.
* [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) installed and configured
* [Git Installed](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## Deployment Instructions

1. Create a new directory, navigate to that directory in a terminal and clone the GitHub repository:
    ``` 
    git clone git@github.com:ajayv-AWS/serverless_pattern_cloudFormation.git
    ```
2. Change directory to the pattern directory:
    ```
    cd serverless_pattern_cloudFormation
    ```

3. From the command line, use terraform to deploy the AWS resources for the pattern as specified in the SNS-Slck-Teams-integration-cfn.yaml file:
    ```
    aws cloudformation create-stack --stack-name myteststack --template-body file://SNS-Slck-Teams-integration-cfn.yaml
    ```

1. Note the outputs from the CloudFormation deployment process. These contain the resource names and/or ARNs which are used for testing.

## How it works

CloudFormation checks the resources defined in the SNS-Slck-Teams-integration-cfn.yaml and deploys the resources in your AWS account using the credentials and in the region configured on your system when you setup AWS CLI profile.
It will created a SNS topic which you can use to publish notifications to your Slack/Teams channel. A Lambda function which will process the SNS message and pass it to the Slack/Teams webhook. You can customise the code to apply additional formatting as per your usecase.

## Testing

Publish a message from AWS Console or by CLI.

Example using CLI:

aws sns publish --topic-arn ENTER_YOUR_SNS_TOPIC_ARN --subject testSubject --message testMessage

## Cleanup
 
1. Delete the stack
    ```
    aws cloudformation delete-stack --stack-name stackName
    ```
----
Copyright 2023 Amazon.com, Inc. or its affiliates. All Rights Reserved.

SPDX-License-Identifier: MIT-0