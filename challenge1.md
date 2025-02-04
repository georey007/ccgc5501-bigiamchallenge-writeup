## Challenge number
1
## Challenge Statement
Buckets of Fun
## IAM Policy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::thebigiamchallenge-storage-9979f4b/*"
        },
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::thebigiamchallenge-storage-9979f4b",
            "Condition": {
                "StringLike": {
                    "s3:prefix": "files/*"
                }
            }
        }
    ]
}
Close
### Write a short analysis about the IAM policy here

The policy permits access to `s3:GetObject`, allowing the retrieval of specific objects, but denies access to `s3:ListBucket`, meaning I couldn't list the objects in the bucket. It grants the ability to fetch specific objects from the S3 bucket `thebigiamchallenge-storage-9979f4b` while blocking the ability to list its contents. This configuration enables object retrieval but restricts listing, requiring reliance on guessing or obtaining the object key through other methods.
## Solution
The policy enables me to retrieve specific objects from the S3 bucket `thebigiamchallenge-storage-9979f4b`, but it blocks me from listing the bucket's contents. It grants object retrieval access while denying the ability to list objects. This setup forces reliance on guessing or obtaining the object key through other means. The IAM policy permits the `s3:GetObject` action for objects in the bucket but denies the `s3:ListBucket` permission. As a result, I cannot list the bucket's contents but can access objects if I know their exact names. To list the details in the `/files` directory, I would need to use the allowed prefix condition to explore objects within that specific path.
# aws s3 ls thebigiamchallenge-storage-9979f4b/files/
Copy the specific file (flag1.txt) and store it in /tmp/flag1.txt
# aws s3 cp s3://thebigiamchallenge-storage-9979f4b/files/flag1.txt /tmp/flag1.txt
And to display the content,
# cat /tmp/flag1.txt

## Reflection
The first step I took was to carefully review the IAM policy to understand the permissions and restrictions it enforced. The most significant challenge I faced was the inability to list the contents of the S3 bucket. While the policy allowed `s3:GetObject` for retrieving objects, it denied `s3:ListBucket`, preventing me from discovering what objects were available in the bucket.

The breakthrough occurred when I successfully retrieved the object `text1.txt` by guessing its name. This experience underscored how the restriction on `s3:ListBucket` ensures that users cannot discover objects within the bucket, serving as a critical control for safeguarding sensitive or private data. In situations where even the knowledge of a file's existence could compromise security, this restriction provides an essential layer of protection.
