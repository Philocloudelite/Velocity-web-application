A Pen created at CodePen.io. You can find this one at https://codepen.io/sol0mka/pen/kzyjJ.

 github repo for this pen: https://github.com/legomushroom/velocity



















----
> Title: How to Host a Velocity Website on an AWS EC2 Instance. 


> The Agenda for the Hands on Lab are below

1. Create an S3 bucket and upload the HTML/Website files into a desegnated S3 bucket. When uploading the files ensure that it's not Zipped and you can drag and drop the files by holding shift and selecting all the files or you can manually uploading each (FIle and Folder) into S3.
----Create a bucket called webserver-bucket-en with your first and last initial for example webserver-bucket-en, webserver-bucket-mk, webserver-bucket-pl and etc.
----Open up the bucket and upload the individual velocity website files. (Upload --> Add Files) (Open up the css and js folder and upload the individual files). 


2. Create an IAM role with (S3 full access permission) for your EC2 Instance. This will allow your EC2 Instance to interact with your designated S3 bucket to pull the Website file content. (Tag Value: EC2-to-S3-Access | Role name: EC2-to-S3-Access). 

3. Create a new security group Inbound Rule with SSH, HTTPS and HTTP as the firewall ports/protocols. (Security group name/Descripton: Website-SG) (Source IP address on the Security group should be from your Computer. This is one of the Best Practices/ AWS Well Architected Framework). 

4. Also create a keypair called Webserver-keyPair from the EC2 Management Console.

5. Launch an EC2 instance (Linux 2 AMI) and attach keypair and security group. Also attach the S3 IAM role. (Network: Use the Default Network | Subnet: No-Preference, | Auto-Assign Public IP: Enable | IAM Role: EC2-Role, | Storage: Leave as Default, Tage: Key- Name, Value- Webserver-Instance | Security Group: Select an Existing Security Group called Website-SG | Launch your Instance with the Web-keyPair)

6. Now use Putty to SSH into the EC2 Instance to access the CLI and run the SSH commands below. (Hostname: ec2-user@IPV4ADDRESS | From SSH -> Auth lod the web-keyPair)


> SSH Commands that will be ran in the EC2 CLI: Also Check the UserData option remeber to attach IAM role for S3

1. sudo su
2. yum update -y
3. yum install httpd -y
4. chkconfig httpd on
5. cd /var/www/html 
6. aws s3 sync s3://remote_S3_bucket local_directory | aws s3 sync s3://cloudelite-source007 /var/www/html
7. run the command [ls] (To view a list of your directory)
8. run the command [service httpd start] (This Starts the web server service on the EC2 Instance)
9. Search the IP address of your Instance in your browser 

On step (6) from above the sync keyword copies/duplicates the files from the S3 bucket to your EC2 instance html path/ sub-folder directory. (replace <remote_S3_bucket> with the name of your S3 bucket and <local_directory> with the directory you want to copy the Velocity files to [/var/www/html]).
---

> Optional commands to run in the EC2 CLI --> run the commands one at a time [whoami, yum update -y, pwd, ps -ef]

[User data Option]
#!/bin/bash
sudo su
yum update -y
yum install httpd -y
chkconfig httpd on
cd /var/www/html 
aws s3 sync s3://cloudelite-source007 /var/www/html

-------

>>>

> https://learn.acloud.guru/handson/8a73c444-d5a3-461a-81fd-0cb4f0a56103

> https://learn.acloud.guru/handson/c0ad833c-b48f-4072-8c9a-13f0358e0666

> https://learn.acloud.guru/handson/7e6eecaa-283a-46d2-a1ad-8ec41c198250







