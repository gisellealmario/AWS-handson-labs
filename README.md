Working in a medium size company, 2 developers, user1 need frequest access which need a policy called S3RestrictedPolicy, usr 2 needs temporary access which needs Role S3RestrictedRole.

Perform the following tasks:

Create the S3RestrictedPolicy IAM policy. Ensure only the appconfig buckets are accessible.
![create policy for s3](https://github.com/user-attachments/assets/7d6c5cb8-54ba-47e4-a840-73a50f2a8635)
Select the S3 service and all S3 actions.
Select all resources except bucket.
![insert bucket arns](https://github.com/user-attachments/assets/a49522ce-a273-4ff7-aa32-219622c0e2ee)
Add the appconfig bucket names to the policy.
![bucket names](https://github.com/user-attachments/assets/b673f71c-9c9e-41bd-aa7c-562a231285e5)
Make sure the bucket names are there


Perform the following tasks:

Create the S3RestrictedRole IAM role.
![create role](https://github.com/user-attachments/assets/9c7f2c15-b262-4c58-9e19-8fcafa0f3fc2)
Set the trusted entity to AWS account. Copy the user 2 ARN

![copy the user2 arn](https://github.com/user-attachments/assets/7b61857e-ef98-4706-bfd8-e772d4acbad4)

Edit the trust policy then paste the arn of user 2
![edit trust policy](https://github.com/user-attachments/assets/85e7a156-d92c-43de-972b-6fb05e06232d)
![change the arn from s3restrictedRole](https://github.com/user-attachments/assets/f047dc4a-3502-460c-9ce8-4eef2a4cb12c)

Test IAM Policy and Role Configuration
Perform the following tasks:
Attach the S3RestrictedPolicy to the user1. 
![attach policy to user1](https://github.com/user-attachments/assets/de42f78a-a75c-4639-b6a3-d616615733e4)

When user1 is logged in we shoukd see that they don't have permission to customer bucket but can access appconfig bucket, they can also access instances.
![user1 doesn't have permission to customer bucket](https://github.com/user-attachments/assets/5221cec3-cbf8-4a93-955c-ba595df521a9)
![user1 has permission to bucket appconfig](https://github.com/user-attachments/assets/ba5cb3c3-3204-4b6c-98f1-b13c0e28dcd3)
![user1 has permission to ec2](https://github.com/user-attachments/assets/2ecb576f-af92-4390-aab1-7ea7223c71c3)

When user2 is logged in we should see that they don't have access to any of the buckets and they need to Switch Role in order for them to see the buckets. They can also access instances.
![user2 don't have permission to buckets](https://github.com/user-attachments/assets/62e18273-3ece-4e5a-a74f-a30a71390d7a)
Switch to S3RestrictedRole
![Switch Role](https://github.com/user-attachments/assets/175cb92b-6f5d-4187-b4e9-a19b8b26ecdb)
![Role switched to S3RestrictedRole](https://github.com/user-attachments/assets/d587b3da-d643-420a-a7c3-612a37a7cc90)

