# copy the contents of sample.md to start# copy the contents of sample.md to start
## Challenge number
3
## Challenge Statement
Enable Push Notifications
## IAM Policy
{
    "Version": "2008-10-17",
    "Id": "Statement1",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "SNS:Subscribe",
            "Resource": "arn:aws:sns:us-east-1:092297851374:TBICWizPushNotifications",
            "Condition": {
                "StringLike": {
                    "sns:Endpoint": "*@tbic.wiz.io"
                }
            }
        }
    ]
}
Close
### Write a short analysis about the IAM policy here
This IAM policy allows any AWS principal to subscribe to the SNS topic `TBICWizPushNotifications`, provided the subscription endpoint matches the `*@tbic.wiz.io` pattern. While the condition limits access to specific domains, the wide `Principal: "*"` grants unrestricted access to all AWS entities, potentially posing a security risk.
## Solution
The solution involves subscribing to an SNS topic using the https protocol, with an endpoint matching the allowed pattern (*@tbic.wiz.io). This ensures successful subscription by satisfying the SNS topic's resource-based policy
## Reflection
Challenge 3 emphasizes the critical understanding of AWS SNS and IAM policies, particularly in handling resource-based permissions and subscriptions. It underscores the importance of configuring policies that restrict access to specific domains or endpoints, while also ensuring a balance between security and functionality in cloud resources.
