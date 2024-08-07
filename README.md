Creating a fully working serverless reminder application using S3, Lambda, API Gateway, Step Functions, Simple Email Service, and Simple Notification Service. 

Note: Make sure you're in the N. Virginia (us-east-1) region throughout the lab.

https://github.com/ACloudGuru-Resources/lab-building-a-serverless-application-using-step-functions-api-gateway-lambda-and-s3-in-aws
download the code 

Objective 1: Verify an Email Address in Simple Email Service (SES)
Open Simple Email Service in a new tab by typing Simple Email Service into the search bar at the top of the screen. Right-click Amazon Simple Email Service from the drop-down menu, and select Open Link in New Tab.

In the Amazon Simple Email Service (SES) console, Click the three horizontal line icon in the top left and choose Configuration - Identities.

Click Create identity.
<img width="1035" alt="Screenshot 2024-08-01 at 2 33 43 PM" src="https://github.com/user-attachments/assets/91a02fab-13b7-4bd8-8ca6-646898e3ff9e">

Choose Email address, enter your personal email address (or an email address you created specifically for this hands-on lab). Click Create identity. (Note outlook accounts do not seem to work well with this lab but gmail does).
<img width="1095" alt="Screenshot 2024-08-01 at 2 34 22 PM" src="https://github.com/user-attachments/assets/8f364e8b-5478-4960-8216-2fde9a87de24">

In a new browser tab or email client, navigate to your email, open the Amazon SES verification email, and click the provided link.

Note: Check your spam mail if you do not see it in your inbox.

You should see a Congratulations! page that confirms you successfully verified your email address.
![Screenshot 2024-08-01 at 2 34 38 PM](https://github.com/user-attachments/assets/4d7913f6-c531-479d-8fe7-74d4a3f5182b)

Return to the AWS SES console tab.

You should now see Verified under Identity status. (Note: You may need to refresh the page.)

Objective 2: Create the Email Lambda Function
In the GitHub repo GitHub Repo. Download the files as a .zip and expand this on your machine. Using a text editor such as VSCode open the file, email_reminder.py.

Return to your first tab, and in the AWS Management Console, navigate to Lambda by typing Lambda in the search bar at the top of the screen. Select Lambda from the drop-down menu.

In the AWS Lambda console, click Create function.
<img width="1036" alt="Screenshot 2024-08-01 at 2 42 30 PM" src="https://github.com/user-attachments/assets/8d9fa42d-6feb-412c-85c9-750431bf9e1e">

Leave the Author from scratch option selected, and then set the following values:

Function name: email
Runtime: Python 3.12
Expand Change default execution role by clicking the arrow next to it.

Below Execution role, select Use an existing role.
<img width="1042" alt="Screenshot 2024-08-01 at 2 43 04 PM" src="https://github.com/user-attachments/assets/8ceb6d4d-3239-489b-9dea-81d41a5607fd">

Once you select that, click into the empty drop-down menu that appears below Existing role.

Select LambdaRuntimeRole from the drop-down menu.

Click Create function at the bottom of the page.

Scroll down to Code source and from the Environment file list on the left, click lambda_function.py to display the function code.

Delete all of the provided code.

Return to your visual editor with the email_reminder.py file from the GitHub repo open.

Copy all of the code to your clipboard.

Return to the Lambda console in your first tab, and paste the copied code into lambda_function.py.

Within the lambda_function code, on line 3, delete the YOUR_SES_VERIFIED_EMAIL placeholder, and type in the email you just used, making sure to leave the single quotes around it.
<img width="1037" alt="Screenshot 2024-08-01 at 2 44 17 PM" src="https://github.com/user-attachments/assets/4fa39944-551b-4199-b17e-bfccfa01763d">

Click Deploy in the Code source menu bar above the code.

Your changes have now been deployed.

Scroll up on the same page to the Function Overview section, and copy the Function ARN by clicking the copy icon next to it, and paste it into a text file for later use in the lab.

Objective 3: Create a Step Function State Machine
Open the AWS Step Functions console in a new tab by typing Step Functions into the search bar at the top of the screen. Right-click Step Functions from the drop-down menu, and select Open Link in New Tab.

In the AWS Step Functions console tab, click Get started.

In the pop-up window, click Create your own to create your own workflow from scratch.
<img width="808" alt="Screenshot 2024-08-01 at 2 44 47 PM" src="https://github.com/user-attachments/assets/3e691d53-6b1e-482a-bb0f-1c4f7717be67">

On the new page, click on Code and delete all of the provided code.

Open the step-function-template.json file to your text editor.

Copy all of the code to your clipboard.

Return to the Step Functions console tab, and paste the code on the left side of the screen.
<img width="1057" alt="Screenshot 2024-08-01 at 2 46 05 PM" src="https://github.com/user-attachments/assets/6b296451-c354-4fa4-96ec-4529504fefca">

On line 23, replace the EMAIL_REMINDER_ARN placeholder value with the copied ARN for email that you copied over onto a text file earlier, being sure to leave the double quotes around the ARN.
<img width="305" alt="Screenshot 2024-08-01 at 2 46 51 PM" src="https://github.com/user-attachments/assets/2d2708ef-daa4-4346-9426-b58c351753b2">
<img width="686" alt="Screenshot 2024-08-01 at 2 48 04 PM" src="https://github.com/user-attachments/assets/d539d275-5581-4872-8cb6-591d5bb0d7af">

Click on the Config button at the top.

Leave the default name MyStateMachine.
<img width="1396" alt="Screenshot 2024-08-01 at 2 48 40 PM" src="https://github.com/user-attachments/assets/d98b2238-c8a1-4156-83b7-36083a2ffada">

Under Permissions, click the dropdown for the Execution role and select RoleForStepFunction under Existing roles.

Scroll to the top and click on Create.

Your state machine should now be created.

On the MyStateMachine page, under Details, copy the ARN to your clipboard or text file. (If you are still in the State machine configuration page click on exit at the top)

Objective 4: Create the api_handler Lambda Function
Scroll up to the navigation line at the top of the page, click Lambda to return to the main Lambda console.

Click Create function.
<img width="1386" alt="Screenshot 2024-08-01 at 2 49 27 PM" src="https://github.com/user-attachments/assets/0b16a206-27d6-4183-a512-06acb4934f42">

Leave the Author from scratch option selected, and then set the following values:

Function name: api_handler
Runtime: Python 3.12
Expand Change default execution role by clicking the arrow next to it.

Below Execution role, select Use an existing role.

Once you select that, click into the empty drop-down menu that appears below Existing role.
<img width="1307" alt="Screenshot 2024-08-01 at 2 49 49 PM" src="https://github.com/user-attachments/assets/603d6d3f-ec9e-49e0-869d-d23576bc33cc">

Select LambdaRuntimeRole from the drop-down menu.

Click Create function at the bottom of the page.

Scroll down to Code source and from the Environment file list on the left, click lambda_function.py to display the function code.

Delete all of the provided code.

Open the api_handler.py file from the files you downloaded into your text editor..

Copy all of the code to your clipboard.

Return to the AWS Lambda console in your first tab, and paste the copied code in to the lambda_function.py function.

On line 6 copy the MyStateMachine arn from your clipboard or text editor making sure to leave ’ each side of the arn.
<img width="1152" alt="Screenshot 2024-08-01 at 2 51 10 PM" src="https://github.com/user-attachments/assets/9363c3bc-e098-4db1-be8c-3a52edf7fe94">

<img width="1396" alt="Screenshot 2024-08-01 at 2 51 41 PM" src="https://github.com/user-attachments/assets/7ffc47cb-0ea7-43c4-99e3-55e4b2cae724">

Click Deploy. Keep this tab open.

Objective 5: Create the API Gateway
Open the Amazon API Gateway console in a new tab by typing API Gateway into the search bar at the top of the screen. Right-click API Gateway from the drop-down menu, and select Open Link in New Tab.

In your Amazon API Gateway console tab, scroll down to REST API (the one that does not say Private), and then select Build.
<img width="1373" alt="Screenshot 2024-08-01 at 2 52 10 PM" src="https://github.com/user-attachments/assets/23466fd4-0188-47f0-8869-4831cebf1f19">

Under API Details, select New API.
<img width="1394" alt="Screenshot 2024-08-01 at 2 52 28 PM" src="https://github.com/user-attachments/assets/399072f3-203d-4172-b745-bb3c4959ac94">

Then configure the following values:

API name: reminders
Leave Description blank.
Endpoint Type: Regional
Click Create API at the bottom of the screen.

You should now be in your API Gateway, and you will see that you don't have any methods defined for the resource.

You should now see the Resources page. Click Create Resource.
<img width="1150" alt="Screenshot 2024-08-01 at 2 52 41 PM" src="https://github.com/user-attachments/assets/b57ba434-fcdd-42ba-b051-d8f3a6faa794">

Under Resource Name, enter reminders.
<img width="1370" alt="Screenshot 2024-08-01 at 2 52 55 PM" src="https://github.com/user-attachments/assets/634daa34-4e80-40b7-a87d-3a4817f18b1f">

Select the checkbox next to CORS.

Click Create Resource at the bottom of the page.

You should be back at the Resources page again.

Click Create method.
<img width="1141" alt="Screenshot 2024-08-01 at 2 53 17 PM" src="https://github.com/user-attachments/assets/0cf4610a-4371-4e9b-a24e-540316ffc5f2">

In the dropdown that appears under Method type, select POST and set the following values:
<img width="1387" alt="Screenshot 2024-08-01 at 2 54 34 PM" src="https://github.com/user-attachments/assets/e10c47b6-c0e9-46a3-80cd-9b44779aacc7">

Integration type: Lambda Function
Enable Lambda Proxy integration by clicking the toggle.
Lambda Region: us-east-1
Lambda Function: Start typing, and then select, api_handler.
Click Create method at the bottom of the page.

Back at the Resources page, click Deploy API at the top.
<img width="1148" alt="Screenshot 2024-08-01 at 2 55 10 PM" src="https://github.com/user-attachments/assets/813ccc0a-cda2-47f1-afba-a5872d40fb63">

<img width="1151" alt="Screenshot 2024-08-01 at 2 55 26 PM" src="https://github.com/user-attachments/assets/1da98042-c592-4618-a57e-ee1de047d872">

In the Deploy API pop-up window, set the following values:

Deployment stage: [New Stage]
Stage name: prod
Click Deploy.

Note: You may ignore any Web Application Firewall (WAF) permissions warning messages if received after deployment.

Copy the invoke url into your clipboard or text editor for use in the next objective.
<img width="898" alt="Screenshot 2024-08-01 at 2 55 47 PM" src="https://github.com/user-attachments/assets/d9c074ae-eeab-4662-a0c7-d1cb3c8f8f37">

Objective 6: Create and Test the Static S3 Website
Within the files you downloaded at the start of this lab, navigate to the static website folder.

Open the formlogic.js file in a text editor.

On line 5 of formlogic.js, delete the UPDATETOYOURINVOKEURLENDPOINT placeholder. Paste in the Invoke URL you previously copied from API Gateway, then append the following at the end of the url /reminders.
<img width="1431" alt="Screenshot 2024-08-01 at 2 57 38 PM" src="https://github.com/user-attachments/assets/2dc9e082-b7c7-4aa4-819a-6a261dc8539f">

Save the local file.

Return to your first AWS Management Console tab.

Open the Amazon S3 console in a new tab by typing S3 into the search bar at the top of the screen. Right-click S3 from the drop-down menu, and select Open Link in New Tab.

In the Amazon S3 console, click Create bucket.
<img width="1373" alt="Screenshot 2024-08-01 at 3 01 02 PM" src="https://github.com/user-attachments/assets/0cc3e4c4-4271-4249-8f45-4ac9dd7ebb25">

On the Create bucket page, under Bucket Type leave General Purpose selected and then for Bucket name, enter a globally unique bucket name.

Under Object Ownership, select ACLs enabled, and ensure Bucket owner preferred is selected.
<img width="1391" alt="Screenshot 2024-08-01 at 3 01 48 PM" src="https://github.com/user-attachments/assets/cd491e42-003b-409f-87e4-08b2da750c0b">

Uncheck Block all public access.

Under Block all public access, select I acknowledge that the current settings might result in this bucket and the objects within becoming public.
<img width="1378" alt="Screenshot 2024-08-01 at 3 02 14 PM" src="https://github.com/user-attachments/assets/6c31151c-c2fb-4644-9c58-aa045ac82b8b">

Leave the other defaults, scroll down, and click Create bucket.

Select the new bucket under Buckets to open it.

On the bucket page, click Upload.
<img width="1217" alt="Screenshot 2024-08-01 at 3 15 31 PM" src="https://github.com/user-attachments/assets/4bce4cce-5899-4a33-bbad-121cae7f2923">

On the Upload page, click Add files and select all of your local files from the static_website folder, and click Open. Or, drag all of your local files from the static_website folder into the Drag and drop box under Upload.

cat.png
error.html
formlogic.js
IMG_0991.jpg
index.html
main.css
Once all of the files have been added, scroll down, and click Permissions to expand the access options.

Under Predefined ACLs, select Grant public-read access.

Under Grant public-read access, select I understand the risk of granting public-read access to the specified objects.
<img width="1383" alt="Screenshot 2024-08-01 at 3 16 22 PM" src="https://github.com/user-attachments/assets/eaf91dbc-ddf4-4168-8948-513fcb87e912">

Click Upload at the bottom of the page.

Once you see the uploads have succeeded, click Close in the top right-hand corner of the page.

Click on the Properties tab under the bucket name.

Scroll down to Static website hosting, and click Edit.
<img width="1402" alt="Screenshot 2024-08-01 at 3 17 48 PM" src="https://github.com/user-attachments/assets/144c2aed-e0f1-4486-ad81-5f494b3bf14b">

On the Edit static website hosting page, under Static website hosting, select Enable.
<img width="1396" alt="Screenshot 2024-08-01 at 3 18 30 PM" src="https://github.com/user-attachments/assets/6fccfb90-8794-4e7f-9c1b-9fbe045a3d4c">

Set the following values:

Index document: index.html
Error document: error.html
Click Save changes at the bottom of the page.

Scroll down again to Static website hosting, and click the URL below Bucket website endpoint to access the webpage.

Once you are on the static website, to test the service's functionality, set the following values:

Seconds to wait: 1
Message: Hello!
someone@something.com: Your personal email address (This has to be the same one you verified with Simple Email Service earlier.)
Under Reminder Type, select email.

You should see Looks ok. But check the result below! above the Required sections, and you should see {"Status":"Success"} at the bottom of the page.

Navigate to your AWS Step Functions console tab.

In the Executions section, click on the refresh icon.
<img width="1160" alt="Screenshot 2024-08-01 at 3 23 43 PM" src="https://github.com/user-attachments/assets/1cad35bd-2a00-4586-9659-12f202d77cc8">

You should see at least one execution displayed.

<img width="690" alt="Screenshot 2024-08-01 at 3 26 20 PM" src="https://github.com/user-attachments/assets/0a63f359-d386-40fc-98d5-ab7bb1c5e0fc">



Click on one of the executions.

Scroll down to Graph view to view the event's visual workflow.

In a new browser tab or email client, navigate to your email. You should now see a reminder email from the service.
