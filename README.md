Using the information from the createstack.json file, create a CloudFormation stack named cfnlab.
![Screenshot 2024-07-18 at 3 24 32 PM](https://github.com/user-attachments/assets/789f4b1a-0864-4f34-a84f-6588ed758428)
After creating the stack, click edit in Application composer and add this code block

`{
    "Resources": {
        "catpics": {
            "Type": "AWS::S3::Bucket"
        }
    }
}`

![creating s3 bucket canmed catpics](https://github.com/user-attachments/assets/019b4406-46c7-4d26-8e01-10f5d3670fa0)
click create template and keep clicking next and submit till the template is created
![Screenshot 2024-07-18 at 3 24 04 PM](https://github.com/user-attachments/assets/6b8bc539-a3c1-4ba8-a686-ad1f1cb53607)
![created catpics s3](https://github.com/user-attachments/assets/3261a0ca-e3a1-4fda-9ac4-31b6c834902f)
check the resources under the cfnlab stack, as you can see it created an s3 bucket named catpics
![resources s3 catpics](https://github.com/user-attachments/assets/117f9d6a-2728-45f3-97c4-81bbd0cd0781)


Using the following code block, update the CloudFormation stack.

`{
    "Resources": {
        "catpics": {
            "Type": "AWS::S3::Bucket"
        },
        "dogpics": {
            "Type": "AWS::S3::Bucket"
        }
    }
}`

Update the CloudFormation stack to observe how resources are added and removed.
![Screenshot 2024-07-18 at 3 26 27 PM](https://github.com/user-attachments/assets/aa9ab58e-72ef-43dc-acbd-2891cb122ca4)
![Screenshot 2024-07-18 at 3 26 41 PM](https://github.com/user-attachments/assets/942bf9bd-055a-4244-a820-ccbeca73db3f)
![Screenshot 2024-07-18 at 3 27 48 PM](https://github.com/user-attachments/assets/9d4c0467-4577-4373-b1ee-e7d6cd6a42f6)
Just before you submit the changes, scroll at the very bottom and you will see the change set preview, it will show that theres a new s3 bucket that will be created names dogpics
![Screenshot 2024-07-18 at 3 28 53 PM](https://github.com/user-attachments/assets/178d3cf3-8c2f-4313-9aa9-0e4979b2c1d7)
When you check the resource that's created, the dogpics in added
![Screenshot 2024-07-18 at 3 29 56 PM](https://github.com/user-attachments/assets/1c74e250-3caf-420c-836f-417711eac885)

Update the CloudFormation Stack to Rename the S3 Bucket
Follow the last steps and use this code block
`{
    "Resources": {
        "catpics": {
            "Type": "AWS::S3::Bucket",
            "Properties": {
                "BucketName": "catsareawesome123"
            }
        },
        "dogpics": {
            "Type": "AWS::S3::Bucket"
        }
    }
}`

Update cfnlab again, replacing the current template with the modified template.
Check the preview and you will see that the replacement is 'true' which means the old resource will be deleted because you cannot rename an s3.
![Screenshot 2024-07-18 at 3 36 59 PM](https://github.com/user-attachments/assets/4b8d2705-8dca-432c-b8a6-b048df1d9f39)
submit and you will see that the old s3 will be deleted
![Screenshot 2024-07-18 at 3 38 50 PM](https://github.com/user-attachments/assets/8a1a7490-02af-44e9-90a9-6c5318474c75)

go to your s3 buckets and will show you the resources that was created
![Screenshot 2024-07-18 at 3 39 33 PM](https://github.com/user-attachments/assets/533762cd-e40f-4e52-867c-c0d37b5fd01a)

