Project 1: Create a static website using aws S3 and redirects to an http error.
Objective:
Create and configure a simple static website. It will through configuring that static website with a custom error page. To demonstrate how to create a cost-efficient website hosting for sites that consist of files like HTML, CSS, JavaScript, fonts, and images.
Services Used:
Amazon S3
**Diagram:**
 
![image](https://user-images.githubusercontent.com/85041307/121835337-492c6280-cc8e-11eb-9760-093b59c8789c.png)


Log in to the AWS console.
S3 is a global service. 
Go to S3 service
 ![image](https://user-images.githubusercontent.com/85041307/121835430-855fc300-cc8e-11eb-82a7-d83e76eaa666.png)

Create S3 Bucket
 ![image](https://user-images.githubusercontent.com/85041307/121835441-8abd0d80-cc8e-11eb-9c37-f613ce3f79a7.png)

Navigate to S3.
Click Create bucket.
 ![image](https://user-images.githubusercontent.com/85041307/121835451-901a5800-cc8e-11eb-9130-e1dc50f0b602.png)

Set the following values:
Bucket name: prafulpatel2021 with the AWS account number or another series of numbers at the end to make it globally unique
Region: US East (N. Virginia) us-east-1
In the Bucket settings for Block Public Access section, un-check Block all public access.
 ![image](https://user-images.githubusercontent.com/85041307/121835468-9c061a00-cc8e-11eb-88b4-dd37c571a7f2.png)

Ensure all four permissions restrictions beneath it are also un-checked.
Check the box to acknowledge that turning off all public access might result in the bucket and its objects becoming public.
Leave the rest of the settings as their defaults.
Click Create bucket.
 ![image](https://user-images.githubusercontent.com/85041307/121835487-a7f1dc00-cc8e-11eb-965e-499357597cd7.png)

Select the bucket name.
 
Click Upload.
 ![image](https://user-images.githubusercontent.com/85041307/121835502-ae805380-cc8e-11eb-98fb-1de9f76cd462.png)


Click Add files, and upload your own or the error.html and index.html
Leave the rest of the settings as their defaults.
 ![image](https://user-images.githubusercontent.com/85041307/121835516-b6d88e80-cc8e-11eb-9a8d-9d1026492fc5.png)

Click Upload.
 
 ![image](https://user-images.githubusercontent.com/85041307/121835531-c061f680-cc8e-11eb-91ec-858ee749aae9.png)
 ![image](https://user-images.githubusercontent.com/85041307/121835539-c6f06e00-cc8e-11eb-8249-e2330c932d69.png)



Click Exit in the upper right.

Enable Static Website Hosting


Click the Properties tab.
 ![image](https://user-images.githubusercontent.com/85041307/121835548-cf48a900-cc8e-11eb-8f0a-4e6a10f585e5.png)

Scroll to the bottom of the screen to find the Static website hosting section.
![image](https://user-images.githubusercontent.com/85041307/121835557-d53e8a00-cc8e-11eb-8a29-73a9cf2ca32a.png)

 
On the right in the Static website hosting section, click Edit.
![image](https://user-images.githubusercontent.com/85041307/121835575-df608880-cc8e-11eb-9798-efc2b735ef00.png)

 
On the Edit static website hosting page, set the following values:

Static website hosting: Enable
Hosting type: Host a static website
Index document: index.html
Error document: error.html
 ![image](https://user-images.githubusercontent.com/85041307/121835605-f30bef00-cc8e-11eb-95a7-5412c56a8069.png)

Click Save changes.
 ![image](https://user-images.githubusercontent.com/85041307/121835612-f901d000-cc8e-11eb-81c1-baf1f52acda3.png)

Scroll back down to the Static website hosting section.
 ![image](https://user-images.githubusercontent.com/85041307/121835630-00c17480-cc8f-11eb-9483-15a8b2ce449d.png)

Open the listed endpoint URL in a new browser tab. We'll see a 403 Forbidden error message.
![image](https://user-images.githubusercontent.com/85041307/121835653-0b7c0980-cc8f-11eb-830a-4056999d99c1.png)

 

Apply Bucket Policy
Back in S3, click the Permissions tab.
 ![image](https://user-images.githubusercontent.com/85041307/121835665-120a8100-cc8f-11eb-9d8f-259853094a74.png)

In the Bucket policy section, click Edit.
 ![image](https://user-images.githubusercontent.com/85041307/121835679-16369e80-cc8f-11eb-82b6-0b9068c48a24.png)

In the Policy box, enter the following JSON statement (replacing <BUCKET_ARN> with the bucket ARN provided right above the Policy box):
Generate a Bucket policy using Policy generator

Find the ARN and copy
 ![image](https://user-images.githubusercontent.com/85041307/121835686-1a62bc00-cc8f-11eb-82c9-c58b4bb6e88f.png)

Go to Policy Generator
 
 ![image](https://user-images.githubusercontent.com/85041307/121835706-22226080-cc8f-11eb-83b9-a1d459b6d0b8.png)

 ![image](https://user-images.githubusercontent.com/85041307/121835714-26e71480-cc8f-11eb-9a7d-19e501736d1d.png)
 ![image](https://user-images.githubusercontent.com/85041307/121835719-2b133200-cc8f-11eb-8897-6dff3287cfc2.png)
 ![image](https://user-images.githubusercontent.com/85041307/121835723-2f3f4f80-cc8f-11eb-9ebd-49d8b71411a6.png)
 ![image](https://user-images.githubusercontent.com/85041307/121835728-34040380-cc8f-11eb-8084-9fcefd8cfdcf.png)
 
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
![image](https://user-images.githubusercontent.com/85041307/121835757-44b47980-cc8f-11eb-8856-f5fe3c7d6d06.png)
 

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
 ![image](https://user-images.githubusercontent.com/85041307/121835777-4d0cb480-cc8f-11eb-94aa-088c0a4c79a8.png)
 ![image](https://user-images.githubusercontent.com/85041307/121835782-50a03b80-cc8f-11eb-8a22-43d6d54288a1.png)
![image](https://user-images.githubusercontent.com/85041307/121835789-5564ef80-cc8f-11eb-9429-313e047ebfc7.png)


 
 
Refresh the browser tab with the static website (the endpoint URL we opened a minute ago). This time, it should load the site correctly.
Test Web URL:
http://prafulpatel2021.s3-website-us-east-1.amazonaws.com
 
After Refresh Verify that the static web page URL is loaded correctly and web page is displayed
 
 ![image](https://user-images.githubusercontent.com/85041307/121835859-7af1f900-cc8f-11eb-9037-4e061a45c911.png)
 ![image](https://user-images.githubusercontent.com/85041307/121835876-8513f780-cc8f-11eb-9dc2-83270d9bab7d.png)


Add a / at the end of the URL and some random letters (anything that's knowingly an error). This will display our error.html info.
Test Web URL:
 ![image](https://user-images.githubusercontent.com/85041307/121835883-89d8ab80-cc8f-11eb-8000-4d2cebdcbdd2.png)


Do Refresh the URL after entering /222 and validate that the Error.html page is displayed
Redirect for an HTTP error
http://prafulpatel2021.s3-website-us-east-1.amazonaws.com/2343
 
![image](https://user-images.githubusercontent.com/85041307/121835890-8fce8c80-cc8f-11eb-8ab6-6f69f9510dfa.png)

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

