
# Cloudfoxable 4

## Challenge Statement
It's another secret 

### What was this challenge about?
```
For this lab, I needed to access a hidden "flag" stored in AWS Systems Manager (SSM) by working with IAM roles and permissions. The main focus was learning how to:

1. Assume an IAM role (named "Ertz") from a starter account
2. Fix permission issues when role assumption fails.
3. Retrieve secrets securely using AWS CLI
```

## My Initial Setup
I began as a `non-root-user` with Admin access, but ran into an issue—the account lacked permission to assume the `Ertz` role. The role's trust policy only allowed the `ctf-starting-user` to take over.

## Solution
### 1. First Attempt (Failed)  
I tried running:  

```  
aws --profile cloudfoxable sts assume-role --role-arn arn:aws:iam::307946660251:role/Ertz --role-session-name Ertz  
```  

However, access was denied. After reviewing the role’s trust policy, I realized my user (`non-root-user`) wasn’t listed as an authorized principal.  

### 2. Updating the Trust Policy  
To fix this, I modified the `Ertz` role’s trust policy to include my user:  

```  
{  
  "Version": "2012-10-17",  
  "Statement": [{  
    "Effect": "Allow",  
    "Principal": {  
      "AWS": [  
        "arn:aws:iam::307946660251:user/ctf-starting-user",  
        "arn:aws:iam::307946660251:user/non-root-user"  
      ]  
    },  
    "Action": "sts:AssumeRole"  
  }]  
}  
```  

### 3. Assuming the Role Successfully  
With the updated policy, I reran the `assume-role` command, and this time it worked! I obtained temporary credentials to act as the `Ertz` role.  

### 4. Retrieving the Secret  
Now that I had `Ertz` permissions, I fetched the secret flag using:  

```  
aws ssm get-parameter --name "/cloudfoxable/flag/its-another-secret" --with-decryption --region us-west-2  
```  

Flag retrieved:  

```  
FLAG{ItsAnotherSecret::ThereWillBeALotOfAssumingRolesInThisCTF}  
```  

### 5. Verifying Permissions  
I confirmed that the `Ertz` role had an attached policy allowing SSM access, which explained why I could retrieve the secret after assuming the role.

## Reflection
* **Biggest Challenge:** Getting the trust policy formatted correctly—I initially had trouble structuring the JSON properly.  
* **Key Breakthrough:** Understanding that I needed to explicitly add my user ARN to the role's trust relationship.  
* **Security Takeaways:** In real AWS environments, always:  
  ```  
  Follow the principle of least privilege (avoid unnecessary Admin access)  
  Regularly audit role trust policies  
  Store secrets securely in SSM or Secrets Manager (never in plaintext!)  
  ```  
This challenge provided hands-on experience with role assumption and trust policies—an essential skill for cloud security!
