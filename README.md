Make sure you are in us-east-1 (N. Virginia) for the lab environment.

The 2 HTML files required from this lab can be downloaded by Saving As these 2 files: index.html and error.html . You will find these files in the following GitHub repository: https://github.com/ACloudGuru-Resources/Course-Certified-Solutions-Architect-Associate/tree/master/labs/creating-a-static-website-using-amazon-s3 .

Note: When creating the bucket, uncheck all four checkboxes on step 3 — Set Permissions. If you skip this step, you will not be allowed to create the bucket policy later. If you made a mistake and created the bucket without unchecking the checkboxes, you may go to Bucket > Permissions > Public access settings > Edit, and uncheck all four restrictions. Then add a bucket policy, go to Bucket > Permissions > Bucket Policy, and add the following JSON statement (replacing <MY_BUCKET> with your bucket name):

```
{
    "Version": "2012-10-17",
    "Id": "Policy1645724938586",
    "Statement": [
        {
            "Sid": "Stmt1645724933619",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "<BUCKET_ARN>/*"
        }
    ]
}
```

Note: You must make sure that the /* is at the end of the ARN.

------------------------------------------------------------

Create an S3 bucket that begins with the name my-bucket (e.g., my-bucket-<ACCOUNT ID>) in the us-east-1 region. When creating the bucket, remember to uncheck the S3 Block Public Access settings. 
![Screenshot 2024-07-17 at 2 04 29 PM](https://github.com/user-attachments/assets/35b98c2a-a0bb-40b9-bbe8-1767b7fed845)

Upload the code for the static site. You will find the code (index.html and error.html) in the following GitHub repository: https://github.com/ACloudGuru-Resources/Course-Certified-Solutions-Architect-Associate/tree/master/labs/creating-a-static-website-using-amazon-s3
![Screenshot 2024-07-17 at 2 04 55 PM](https://github.com/user-attachments/assets/12a7dc6c-abf9-4f1a-ae52-b8ea7c079613)


Enable Static Website Hosting
You can use Amazon S3 to host a static website. On a static website, individual web pages include static content. They might also contain client-side scripts.

To host a static website on Amazon S3, configure an Amazon S3 bucket for website hosting, and then upload your website content to the bucket.
![Screenshot 2024-07-17 at 2 08 43 PM](https://github.com/user-attachments/assets/4d2caa52-e492-41aa-be55-ae70770f1d34)

When you configure a bucket as a static website, you must enable website hosting, set permissions, and create and add an index document.
![Screenshot 2024-07-17 at 2 09 01 PM](https://github.com/user-attachments/assets/d6f215ed-506c-4639-abb6-f2a1adf20aef)

You must ensure that the S3 Block Public Access settings are disabled on the bucket, so that the files in the bucket can be made publicly readable.
![Screenshot 2024-07-17 at 2 09 48 PM](https://github.com/user-attachments/assets/f9925e44-b84e-49f7-ac34-f02a28119990)
Apply Bucket Policy
To make objects in your bucket publicly readable, write a bucket policy that grants everyone s3:GetObject permission.
copy the ARN
![Screenshot 2024-07-17 at 2 09 58 PM](https://github.com/user-attachments/assets/db142468-49c8-4977-b6bb-b112b50906e2)
Paste the ARN and add /* at the end
![editing policy generator](https://github.com/user-attachments/assets/53fb62ca-a937-4947-9ea5-34283a77254f)
Add statement and generate the code, once the code is generated, copy it and paste it on the edit bucket policy then save
![code block](https://github.com/user-attachments/assets/e4230bfb-9ece-4b69-b616-6bf527cd4a0e)

After saving the bucket policy, the webpage should load
![webpage loaded](https://github.com/user-attachments/assets/e6457e49-0120-4f1e-9b31-86d28f4992ad)


Note that AWS will not permit you to create the policy if the S3 Block Public Access settings are still enabled on the bucket.
After disabling the Block Public Access settings, you can add a bucket policy to grant public read access to your bucket. When you grant public read access, anyone on the internet can access your bucket.

