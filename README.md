Creating a fully working serverless reminder application using S3, Lambda, API Gateway, Step Functions, Simple Email Service, and Simple Notification Service. 

Note: Make sure you're in the N. Virginia (us-east-1) region throughout the lab.

https://github.com/ACloudGuru-Resources/lab-building-a-serverless-application-using-step-functions-api-gateway-lambda-and-s3-in-aws
download the code 

Objective 1: Verify an Email Address in Simple Email Service (SES)
Open Simple Email Service in a new tab by typing Simple Email Service into the search bar at the top of the screen. Right-click Amazon Simple Email Service from the drop-down menu, and select Open Link in New Tab.

In the Amazon Simple Email Service (SES) console, Click the three horizontal line icon in the top left and choose Configuration - Identities.

Click Create identity.

Choose Email address, enter your personal email address (or an email address you created specifically for this hands-on lab). Click Create identity. (Note outlook accounts do not seem to work well with this lab but gmail does).

In a new browser tab or email client, navigate to your email, open the Amazon SES verification email, and click the provided link.

Note: Check your spam mail if you do not see it in your inbox.

You should see a Congratulations! page that confirms you successfully verified your email address.

Return to the AWS SES console tab.

You should now see Verified under Identity status. (Note: You may need to refresh the page.)

Objective 2: Create the Email Lambda Function
In the GitHub repo GitHub Repo. Download the files as a .zip and expand this on your machine. Using a text editor such as VSCode open the file, email_reminder.py.

Return to your first tab, and in the AWS Management Console, navigate to Lambda by typing Lambda in the search bar at the top of the screen. Select Lambda from the drop-down menu.

In the AWS Lambda console, click Create function.

Leave the Author from scratch option selected, and then set the following values:

Function name: email
Runtime: Python 3.12
Expand Change default execution role by clicking the arrow next to it.

Below Execution role, select Use an existing role.

Once you select that, click into the empty drop-down menu that appears below Existing role.

Select LambdaRuntimeRole from the drop-down menu.

Click Create function at the bottom of the page.

Scroll down to Code source and from the Environment file list on the left, click lambda_function.py to display the function code.

Delete all of the provided code.

Return to your visual editor with the email_reminder.py file from the GitHub repo open.

Copy all of the code to your clipboard.

Return to the Lambda console in your first tab, and paste the copied code into lambda_function.py.

Within the lambda_function code, on line 3, delete the YOUR_SES_VERIFIED_EMAIL placeholder, and type in the email you just used, making sure to leave the single quotes around it.

Click Deploy in the Code source menu bar above the code.

Your changes have now been deployed.

Scroll up on the same page to the Function Overview section, and copy the Function ARN by clicking the copy icon next to it, and paste it into a text file for later use in the lab.

Objective 3: Create a Step Function State Machine
Open the AWS Step Functions console in a new tab by typing Step Functions into the search bar at the top of the screen. Right-click Step Functions from the drop-down menu, and select Open Link in New Tab.

In the AWS Step Functions console tab, click Get started.

In the pop-up window, click Create your own to create your own workflow from scratch.

On the new page, click on Code and delete all of the provided code.

Open the step-function-template.json file to your text editor.

Copy all of the code to your clipboard.

Return to the Step Functions console tab, and paste the code on the left side of the screen.

On line 23, replace the EMAIL_REMINDER_ARN placeholder value with the copied ARN for email that you copied over onto a text file earlier, being sure to leave the double quotes around the ARN.

Click on the Config button at the top.

Leave the default name MyStateMachine.

Under Permissions, click the dropdown for the Execution role and select RoleForStepFunction under Existing roles.

Scroll to the top and click on Create.

Your state machine should now be created.

On the MyStateMachine page, under Details, copy the ARN to your clipboard or text file. (If you are still in the State machine configuration page click on exit at the top)

Objective 4: Create the api_handler Lambda Function
Scroll up to the navigation line at the top of the page, click Lambda to return to the main Lambda console.

Click Create function.

Leave the Author from scratch option selected, and then set the following values:

Function name: api_handler
Runtime: Python 3.12
Expand Change default execution role by clicking the arrow next to it.

Below Execution role, select Use an existing role.

Once you select that, click into the empty drop-down menu that appears below Existing role.

Select LambdaRuntimeRole from the drop-down menu.

Click Create function at the bottom of the page.

Scroll down to Code source and from the Environment file list on the left, click lambda_function.py to display the function code.

Delete all of the provided code.

Open the api_handler.py file from the files you downloaded into your text editor..

Copy all of the code to your clipboard.

Return to the AWS Lambda console in your first tab, and paste the copied code in to the lambda_function.py function.

On line 6 copy the MyStateMachine arn from your clipboard or text editor making sure to leave ’ each side of the arn.

Click Deploy. Keep this tab open.

Objective 5: Create the API Gateway
Open the Amazon API Gateway console in a new tab by typing API Gateway into the search bar at the top of the screen. Right-click API Gateway from the drop-down menu, and select Open Link in New Tab.

In your Amazon API Gateway console tab, scroll down to REST API (the one that does not say Private), and then select Build.

Under API Details, select New API.

Then configure the following values:

API name: reminders
Leave Description blank.
Endpoint Type: Regional
Click Create API at the bottom of the screen.

You should now be in your API Gateway, and you will see that you don't have any methods defined for the resource.

You should now see the Resources page. Click Create Resource.

Under Resource Name, enter reminders.

Select the checkbox next to CORS.

Click Create Resource at the bottom of the page.

You should be back at the Resources page again.

Click Create method.

In the dropdown that appears under Method type, select POST and set the following values:

Integration type: Lambda Function
Enable Lambda Proxy integration by clicking the toggle.
Lambda Region: us-east-1
Lambda Function: Start typing, and then select, api_handler.
Click Create method at the bottom of the page.

Back at the Resources page, click Deploy API at the top.

In the Deploy API pop-up window, set the following values:

Deployment stage: [New Stage]
Stage name: prod
Click Deploy.

Note: You may ignore any Web Application Firewall (WAF) permissions warning messages if received after deployment.

Copy the invoke url into your clipboard or text editor for use in the next objective.

Objective 6: Create and Test the Static S3 Website
Within the files you downloaded at the start of this lab, navigate to the static website folder.

Open the formlogic.js file in a text editor.

On line 5 of formlogic.js, delete the UPDATETOYOURINVOKEURLENDPOINT placeholder. Paste in the Invoke URL you previously copied from API Gateway, then append the following at the end of the url /reminders.

Save the local file.

Return to your first AWS Management Console tab.

Open the Amazon S3 console in a new tab by typing S3 into the search bar at the top of the screen. Right-click S3 from the drop-down menu, and select Open Link in New Tab.

In the Amazon S3 console, click Create bucket.

On the Create bucket page, under Bucket Type leave General Purpose selected and then for Bucket name, enter a globally unique bucket name.

Under Object Ownership, select ACLs enabled, and ensure Bucket owner preferred is selected.

Uncheck Block all public access.

Under Block all public access, select I acknowledge that the current settings might result in this bucket and the objects within becoming public.

Leave the other defaults, scroll down, and click Create bucket.

Select the new bucket under Buckets to open it.

On the bucket page, click Upload.

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

Click Upload at the bottom of the page.

Once you see the uploads have succeeded, click Close in the top right-hand corner of the page.

Click on the Properties tab under the bucket name.

Scroll down to Static website hosting, and click Edit.

On the Edit static website hosting page, under Static website hosting, select Enable.

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

You should see at least one execution displayed.

Click on one of the executions.

Scroll down to Graph view to view the event's visual workflow.

In a new browser tab or email client, navigate to your email. You should now see a reminder email from the service.
