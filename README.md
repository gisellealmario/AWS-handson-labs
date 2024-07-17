Working in a medium size company, 2 developers, user1 need frequest access which need a policy called S3RestrictedPolicy, usr 2 needs temporary access which needs Role S3RestrictedRole.

Perform the following tasks:

Create the S3RestrictedPolicy IAM policy. Ensure only the appconfig buckets are accessible.
Select the S3 service and all S3 actions.
Select all resources except bucket.
Add the appconfig bucket names to the policy.

Perform the following tasks:

Create the S3RestrictedRole IAM role.
Set the trusted entity to AWS account.
Select bullet next to This account:
For permissions, select the S3RestrictedPolicy.
Update the S3RestrictedRole trusted entity to the user2 arn value.

Test IAM Policy and Role Configuration
Perform the following tasks:

Attach the S3RestrictedPolicy to the user1. Then, log in as user1 and test access.
Log in as user2, assume the S3RestrictedRole and test access.
