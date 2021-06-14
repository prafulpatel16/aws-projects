Project 1: Create a static website using aws S3 and redirects to an http error.
Objective:
Create and configure a simple static website. It will through configuring that static website with a custom error page. To demonstrate how to create a cost-efficient website hosting for sites that consist of files like HTML, CSS, JavaScript, fonts, and images.
Services Used:
Amazon S3
Diagram:
 


Log in to the AWS console.
S3 is a global service. 
Go to S3 service
 
Create S3 Bucket
 
Navigate to S3.
Click Create bucket.
 
Set the following values:
Bucket name: prafulpatel2021 with the AWS account number or another series of numbers at the end to make it globally unique
Region: US East (N. Virginia) us-east-1
In the Bucket settings for Block Public Access section, un-check Block all public access.
 
Ensure all four permissions restrictions beneath it are also un-checked.
Check the box to acknowledge that turning off all public access might result in the bucket and its objects becoming public.
Leave the rest of the settings as their defaults.
Click Create bucket.
 
Select the bucket name.
 
Click Upload.
 

Click Add files, and upload your own or the error.html and index.html
Leave the rest of the settings as their defaults.
 
Click Upload.
 
 

Click Exit in the upper right.

Enable Static Website Hosting


Click the Properties tab.
 
Scroll to the bottom of the screen to find the Static website hosting section.
 
On the right in the Static website hosting section, click Edit.
 
On the Edit static website hosting page, set the following values:

Static website hosting: Enable
Hosting type: Host a static website
Index document: index.html
Error document: error.html
 
Click Save changes.
 
Scroll back down to the Static website hosting section.
 
Open the listed endpoint URL in a new browser tab. We'll see a 403 Forbidden error message.

 

Apply Bucket Policy
Back in S3, click the Permissions tab.
 
In the Bucket policy section, click Edit.
 
In the Policy box, enter the following JSON statement (replacing <BUCKET_ARN> with the bucket ARN provided right above the Policy box):
Generate a Bucket policy using Policy generator

Find the ARN and copy
 
Go to Policy Generator
 
 
 
 

 
{
  "Id": "Policy1623022285875",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1623022231437",
      "Action": [
        "s3:GetObject"
      ],
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::prafulpatel2021",
      "Principal": "*"
    }
  ]
}





{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::prafulpatel2021/*"
        }
    ]
}
 

Note: Ensure the trailing /* is present so the policy applies to all objects within the bucket.
{
  "Id": "Policy1623022285875",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1623022231437",
      "Action": [
        "s3:GetObject"
      ],
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::prafulpatel2021/*¬",
      "Principal": "*"
    }
  ]
}

Click Save changes.
 
 
 
Refresh the browser tab with the static website (the endpoint URL we opened a minute ago). This time, it should load the site correctly.
Test Web URL:
http://prafulpatel2021.s3-website-us-east-1.amazonaws.com
 
After Refresh Verify that the static web page URL is loaded correctly and web page is displayed
 
 
Add a / at the end of the URL and some random letters (anything that's knowingly an error). This will display our error.html info.
Test Web URL:
 

Do Refresh the URL after entering /222 and validate that the Error.html page is displayed
Redirect for an HTTP error
http://prafulpatel2021.s3-website-us-east-1.amazonaws.com/2343
 

Useful resources & Links:
https://github.com/prafulpatel16/aws-projects/tree/main/creating-a-static-webiste-using-aws-s3
https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html


Project 2 : Create a static website using aws S3 with enabling & logging web server traffic logs.

Objective:
To access Logging web traffic
To enable server access logging for your static website bucket
1.	Open the Amazon S3 console at https://console.aws.amazon.com/s3/.
2.	In the same Region where you created the bucket that is configured as a static website, create a bucket for logging, for example logs.example.com.
 
 

3.	Create a folder for the server access logging log files (for example, logs).
When you group your log data files in a folder, they are easier to locate.
 
 
4.	(Optional) If you want to use CloudFront to improve your website performance, create a folder for the CloudFront log files (for example, cdn).
5.	In the Buckets list, choose your bucket.
 
6.	Choose Properties.
 
7.	Under Server access logging, choose Edit.
 
8.	Choose Enable.
 
9.	Under the Target bucket, choose the bucket and folder destination for the server access logs:
•	Browse to the folder and bucket location:
a.	Choose Browse S3.
 
b.	Choose the bucket name, and then choose the logs folder.
c.	Choose Choose path.
•	Enter the S3 bucket path, for example, s3://logs.example.com/logs/.
 
 

10.	Choose Save changes.
 
In your log bucket, you can now access your logs. Amazon S3 writes website access logs to your log bucket every 2 hours.
Verify Output that logs has been collected.
 


Useful Links:
https://docs.aws.amazon.com/AmazonS3/latest/userguide/LoggingWebsiteTraffic.html

