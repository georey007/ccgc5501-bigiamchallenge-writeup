# copy the contents of sample.md to start
## Challenge number
2
## Challenge Statement
Google Analytics
## IAM Policy
{ "Version": "2012-10-17", "Statement": [ { "Effect": "Allow", "Principal": "*", "Action": [ "sqs:SendMessage", "sqs:ReceiveMessage" ], "Resource": "arn:aws:sqs:us-east-1:092297851374:wiz-tbic-analytics-sqs-queue-ca7a1b2" } ] }
### Write a short analysis about the IAM policy here

In this challenge, I understood that the policy allows any principal to send and receive messages from the AWS SQS queue, `wiz-tbic-analytics-sqs-queue-ca7a1b2`, in the `us-east-1` region. What stood out to me was that the policy permits anyone to send and receive messages without any restrictions, which poses a significant security risk. Attackers could easily retrieve messages from the queue, potentially gaining access to sensitive data and exposing it.

## Solution
Detailed steps to the flag I gtot an idea about the aws sqs from https://docs.aws.amazon.com/cli/latest/reference/sqs/receive-message.html From there I found the command to receive messages from an sqs queue aws sqs receive-message --queue-url https://sqs.us-east-1.amazonaws.com/80398EXAMPLE/MyQueue --attribute-names All --message-attribute-names All I made appropriate changes to the command get the message. That message contained the url to the flag.

## Reflection
I began by familiarizing myself with AWS SQS and researched how to use the `receive-message` command to interact with the queue and retrieve messages. The main challenge was figuring out the correct command to fetch the message. After making the necessary adjustments to the command, I successfully received the message, which included a URL pointing to the flag.
