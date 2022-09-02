## Prerequisites
This documents contains the prerequisites to use the [amazon-braket-hybrid-jobs-handler](https://github.com/UST-QuAntiL/amazon-braket-hybrid-jobs-handler) with the [QuantME-Transformation-Framework](https://github.com/UST-QuAntiL/QuantME-TransformationFramework). Also an example use case exists at [Use-Case](https://github.com/SharonNaemi/UseCase).

1) Credentials in AWS
The Boto3 client needs your credentials to access and manage the resources in AWS. Therefore, the public access key as well as the private key must be provided to the workflow. If you don't have any keys, you can create one. 
For futher information please take a look at [How-to-create-or-manage-keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

2) ExecutionRole
In order to allow the creation and management of resources a corresponding role has to be created. This can be easily done when using the Amazon Braket UI to create a hybrid job. AWS will create a default role with the name "AmazonBraketJobsExecutionRole" which allow to create and manage resources outside AWS. But be cautious, the default role will only allow to interact with S3 buckets starting which the prefix "amazon-braket-" in the same region. 

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:PutObject",
                "s3:ListBucket",
                "s3:CreateBucket",
                "s3:PutBucketPublicAccessBlock",
                "s3:PutBucketPolicy"
            ],
            "Resource": "arn:aws:s3:::amazon-braket-*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ecr:GetDownloadUrlForLayer",
                "ecr:BatchGetImage",
                "ecr:BatchCheckLayerAvailability"
            ],
            "Resource": "arn:aws:ecr:*:*:repository/amazon-braket*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ecr:GetAuthorizationToken"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "braket:CancelJob",
                "braket:CancelQuantumTask",
                "braket:CreateJob",
                "braket:CreateQuantumTask",
                "braket:GetDevice",
                "braket:GetJob",
                "braket:GetQuantumTask",
                "braket:SearchDevices",
                "braket:SearchJobs",
                "braket:SearchQuantumTasks",
                "braket:ListTagsForResource",
                "braket:TagResource",
                "braket:UntagResource"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:PassRole"
            ],
            "Resource": "arn:aws:iam::*:role/service-role/AmazonBraketJobsExecutionRole*",
            "Condition": {
                "StringLike": {
                    "iam:PassedToService": [
                        "braket.amazonaws.com"
                    ]
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:ListRoles"
            ],
            "Resource": "arn:aws:iam::*:role/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "logs:GetQueryResults"
            ],
            "Resource": [
                "arn:aws:logs:*:*:log-group:*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "logs:PutLogEvents",
                "logs:CreateLogStream",
                "logs:CreateLogGroup",
                "logs:GetLogEvents",
                "logs:DescribeLogStreams",
                "logs:StartQuery",
                "logs:StopQuery"
            ],
            "Resource": "arn:aws:logs:*:*:log-group:/aws/braket*"
        },
        {
            "Effect": "Allow",
            "Action": "cloudwatch:PutMetricData",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "cloudwatch:namespace": "/aws/braket"
                }
            }
        }
    ]
}

3) Bucket Policy
In order to allow different buckets for Amazon Braket Hybrid Jobs, you can create a bucket policy which allows the interaction with the Amazon Braket service.
 
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "braket.amazonaws.com"
            },
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::amazon-braket-us-east-1-722637487311",
                "arn:aws:s3:::amazon-braket-us-east-1-722637487311/*"
            ]
        }
    ]
}