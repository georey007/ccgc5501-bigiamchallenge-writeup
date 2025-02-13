# Challenge number
4
## Challenge Statement
The challenge requires us to retrieve a flag from an AWS S3 bucket by leveraging the permissions granted in the IAM policy

## IAM Policy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::thebigiamchallenge-admin-storage-abf1321/*"
    },
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::thebigiamchallenge-admin-storage-abf1321",
      "Condition": {
        "StringLike": {
          "s3:prefix": "files/*"
        }
      },
      "ForAllValues:StringLike": {
        "aws:PrincipalArn": "arn:aws:iam::133713713737:user/admin"
      }
    }
  ]
}
### write a short analysis about the IAM policy here
You have permission to perform `s3:GetObject` on all objects within `thebigiamchallenge-admin-storage-abf1321`, allowing files to be downloaded without authentication.  

However, `s3:ListBucket` is restricted and only accessible to `arn:aws:iam::133713713737:user/admin` for files in the `files/` prefix. This means that while listing objects isn't possible, retrieving them is still feasible if their exact names are known.  

An interesting aspect is that public access is allowed for retrieving objects, but listing is restricted to a specific IAM user. This restriction can be bypassed by guessing object names and downloading them directly.

## Solution
Tried listing files in the S3 bucket with:
aws s3 ls s3://thebigiamchallenge-admin-storage-abf1321/files/ --no-sign-request
Since s3:GetObject is unrestricted, attempted to download a guessed file:
aws s3 cp s3://thebigiamchallenge-admin-storage-abf1321/files/flag-as-admin.txt /tmp/ --no-sign-request
Then read the flag using:
cat /tmp/flag-as-admin.txt
The retrieved flag was:
{wiz:principal-arn-is-not-what-you-think}


## Reflection
First, I reviewed the IAM policy to understand the granted permissions. I found that while listing files was restricted, retrieving objects was allowed. 

I attempted to list the files but was blocked due to the restriction. Then, I tried downloading a potential file directly, and it was successful.

### Biggest Challenge:
The restriction on `s3:ListBucket` made it hard to determine which files were available, requiring me to guess the file names.

### How I Overcame the Challenges:
I used the bucket’s naming pattern and common challenge conventions to guess the correct filename. Since `s3:GetObject` was unrestricted, I was able to retrieve the flag.

### Breakthrough:
The realization that `s3:GetObject` was fully open while `s3:ListBucket` was restricted. Knowing I could still access files if I knew their exact names helped me succeed.

### Defensive Lessons:
Public access to `s3:GetObject` should only be allowed when absolutely necessary. While listing restrictions can limit access, they don't prevent downloading if the objects are publicly accessible. Proper authentication and IAM policies should be enforced to prevent unauthorized access, and using AWS S3 Block Public Access settings can further secure assets
