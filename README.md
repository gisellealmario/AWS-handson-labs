Create an S3 Bucket and Enable Replication
Copy the name of the lab-provided appconfigprod1 bucket and use it to create a new S3 bucket in the US West (Oregon) us-west-2 region, replacing appconfigprod1 with appconfigprod2 to ensure it is globally unique.
![change name to prod2](https://github.com/user-attachments/assets/021072ac-8d98-426b-b6a0-decfa7de67b5)
Note: After creating the new bucket, you may receive a warning about system tags; you can safely ignore it.

Enable automatic file replication from the appconfigprod1 S3 bucket to the appconfigprod2 S3 bucket.
![create replication rule for prod1](https://github.com/user-attachments/assets/ed2cba71-ebce-415d-bc6b-240bf07e6ec5)
![edit replication rules](https://github.com/user-attachments/assets/70674930-a7c6-415b-ac0d-b8b7aecc6419)
![enable versioning](https://github.com/user-attachments/assets/f673ffa2-f9b5-495e-b3a1-f25dba96580f)

Test Replication and Observe Results
Upload a file to the appconfigprod1 S3 bucket.
![upload file to appconfigprod1](https://github.com/user-attachments/assets/60269db4-cd0c-4a40-95cb-772e98a6014f)

Ensure the file was automatically replicated to the appconfigprod2 S3 bucket.
![replicated file to the app configprod2](https://github.com/user-attachments/assets/f50c44b9-b40a-4550-9082-ca8bbbb55846)
