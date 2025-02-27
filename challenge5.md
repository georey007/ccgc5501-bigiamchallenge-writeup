Reflection Paper: Setting Up My Personal AWS Environment

Security Measures Implemented

During the setup of my AWS environment, I followed best security practices to ensure the safety and integrity of my account. Below are the key security measures I implemented:

Multi-Factor Authentication (MFA) for Root User and IAM Users:

I enabled MFA for the root user to add an extra layer of security.

MFA was also enabled for the IAM user to prevent unauthorized access.

Root User Access Key Removal:

AWS recommends not using the root user for daily operations.

I ensured that the root user does not have any active access keys to minimize security risks.

Creation of an IAM Admin User:

Instead of using the root account for administrative tasks, I created an IAM user (georgeyuser2) with AdministratorAccess policy.

This user has sufficient privileges to manage AWS resources while ensuring that the root account remains secured.

Implementation of the Principle of Least Privilege:

I limited permissions to only what is necessary.

In the future, I plan to create specific users or roles for different administrative tasks to further reduce security risks.

Password and Access Key Management:

I enforced strong password policies for IAM users.

I avoided long-term access keys and ensured that all credentials are rotated periodically.

Importance of an IAM Admin User Instead of Root User

Although the root user has unrestricted access, it is a best practice to minimize its usage due to the following reasons:

Enhanced Security: The root user has complete control over the account, and any compromise could lead to severe consequences. An IAM admin user reduces the risk by limiting access.

Audit and Monitoring: IAM users have individual credentials, which allows for better tracking and monitoring of activities through AWS CloudTrail.

Controlled Access Management: IAM users and roles provide better control over permissions, allowing for role-based access control (RBAC) instead of an all-powerful root account.


Conclusion

Setting up a personal AWS environment requires a strong focus on security. By implementing best practices such as MFA, restricted root access, and role-based permissions, I have ensured that my AWS account is secure and manageable. Going forward, I will continue to refine my security measures and explore advanced IAM policies to improve access control.
