# Storing-Pharmaceutical-Documents-using-AWS

INTRODUCTION TO CLOUD COMPUTING

The main Aim of this project is Storing Pharmaceutical documents using Amazon web services (AWS). Cloud computing provides services that can store your data, secure it and even launch virtual services remotely on pay as you go pricing. It’s a technology which is used by different big tech companies like Google, Amazon, Microsoft and many more so what makes cloud technology so special?

The answer to this question lies in its history as cloud was first launched in mid 19th century but its growth rate was slow but in 2006 Amazon ecommerce website had lot of traffic running so they needed to think about scalable, cost-effective compute capacity so they jumped to few technologies like Elastic compute cloud (EC2) which basically created virtual machines and simple storage service(S3) basically used for storing data which then they launched Amazon web services. Along the way big firms with money know how to offer this service. Google launched Google Cloud Platform (GCP) in 2008 and Microsoft also launched its platform named Microsoft Azure in 2010. This results in recent years many companies are migrating their data from on-premises towards cloud for on-demand services as you don’t need to maintain any physical hardware. Cloud computing basically reduces Capex (Capital expenditure) as it’s maintained by cloud providers and client only need to pay for OpenX (operational expenditure).

Press enter or click to view image in full size

Source : Google Trends
A Storing Pharmaceutical company documents virtually using AWS is and ingesting, processing and storing pharmacy data using AWS which can helps the company to store and retrieve any amount of data anywhere from the internet which helps them for later inspection. Company will also be allocated different IAM ID’s with access roles assigned as per departments so that they’ll be able to upload documents to AWS.

AWS will also provide security in the form of 11 9’s of durability in S3. The Goal of this project is that this process can be used in India as most Pharmacy companies in India create a bunch of documents and make files of it and they store it in physical lockers which costs space time, money and more so If we use Aws, it’ll all be virtually and procurement cycle will get reduced which helps in cost optimization, reduce time and efforts. Here companies can set data lifecycles with the help of cloud engineers in which they can maintain life expectancy of the document which helps companies to store in a cost-effective manner. Companies can also enable bucket versioning if they have any updated documents so it’ll be updated without deleting previous documents which will help in accidental deletion of documents.

Basically, In Pharmaceutical Company deals with supplier for materials to prepare medicines and then they forward the consignment to the Retailers and then retailers will sell those medicines to the customers so the company have to make tremendous amount of documents to maintain because if there’s any problem after the retailer has sold medicines the company will have to fetch all required documents what went wrong and where it went wrong also there will be different departments in the company and every department employee will have different IDs to upload important documents of the company securely every time they purchased or buy from retailer or supplier and if anything goes wrong they can retrieve those documents anytime they wants with minimal cost which will even help them in disaster recovery ,cyclone prone areas and many other natural activities.

PRE-REQUISITE :

● Should have AWS account or can create new account at console.aws.amazon.com for free tier (you’ll can still be charged for services you use).

● Basic knowledge of Simple storage service (S3), Elastic Compute Cloud (EC2), Virtual Private Cloud (VPC), Identity and access management (IAM). ● Basic understanding of CLI and networking (Firewalls and IP addresses). ● Internet connection is required for your device SOFTWARE.

REQUIREMENTS :

● Amazon Machine Image (AMI) — ubuntu 18.04

● Memory — 1 GiB

● Storage — 8 GB

● Architecture — x86_64


source : Created on draw.io
SYSTEM IMPLEMENTATION

Login to Console.aws.amazon.com and then follow below Instructions :

Step 1 : CREATE VPC

First, we’ll check the Service Health then I’ll be Creating a VPC > Your VPC > Create VPC > VPC and more. Now name your VPC (I choose 2TA-Arch) and leave the remaining settings to default. Now choose availability zone to 1 with 1 public subnet and 1 private subnet. Now click on NAT Gateway and select in 1 AZ (It’ll cost charge). Further select S3 gateway as VPC Endpoints and click on Create VPC.


source : console.aws.amazon.com
Now choose the number of availability zones (AZs) to 1 and Number of public subnets and Number of private subnets to 1.


source : console.aws.amazon.com
Now click on NAT Gateway and select in 1 AZ (It’ll cost charge). Further select S3 gateway as VPC Endpoints and click on Create VPC.


source : console.aws.amazon.com
Now Click on subnets > public subnet (select that) > Actions > Edit subnet settings > select enable auto assign IP for public IPv4 address > Save. Next Click on security groups > Copy security group ID (Default) > Create new security group > select name (add description) > select VPC (which we created earlier) > Add inbound rule 1 (select all traffic and paste the security group ID in source) > Add inbound rule 2 (select ssh and click on My IP) > create security group.

STEP 2: CREATE EC2

In EC2 Instance we’ll have to Create two instances: Public and Private. Public Instance: First Go to EC2 > Instances > Launch an instance. Now name your Instance and select Application and OS Image (Amazon Machine Image to Ubuntu 18.04 > Choose Instance type t2. micro


source : console.aws.amazon.com
Now, add key pair for encryption and decryption > In network settings click on existing security group and select both security groups we created earlier in step 1 in VPC > Leave rest settings to Default and click Launch Instance.


source : console.aws.amazon.com
Private Instance: Perform the same steps as above but the only difference will be selecting only the “default” security group rather than both. When Instances are Launched take Public IP from Public Instance and login to SSH which we’ll cover in Code Implementation Topic Below.

STEP 3 : CREATE IAM ROLES

Identity and access Management is basically who can access what. To create IAM roles kindly follow below steps:

Go to services > Users > Add users and fill Number of Usernames which you want to create and select AWS access type to see how these users will primarily access AWS > Select Any option from Both either programmatic access for AWS, API, CLI, SDK and other development tools and second access for AWS Management Console (I’ll be selecting only AWS management Console Access) > set console password to Autogenerate or custom password > Next.
Press enter or click to view image in full size

source : console.aws.amazon.com
2. Now Add user to groups but before that you need to create group so Give name to group > Add Policies (I have added S3 Full Access Policy and IAM user change password > create > Next to tags.

Press enter or click to view image in full size

source : console.aws.amazon.com
3. In tags we can write the Full name of Employee and their Employee ID’s so that if anything goes wrong, we can track them. After that click on next Review.

Press enter or click to view image in full size

source : console.aws.amazon.com
4. In Review you need to Verify All the details and click on create user (user has successfully created).

Press enter or click to view image in full size

source : console.aws.amazon.com
5) Now you can Email the user login Instruction (.csv file Attached) so that he can able to login and upload data in S3 Bucket as well as he’ll be able to change his password.

Press enter or click to view image in full size

source : console.aws.amazon.com
Email sent to Employee for password reset and use AWS console will look like This.

Press enter or click to view image in full size

source : Email
STEP 4: CREATE S3

Simple Storage Service is blob storage where you can upload and retrieve any amount of data over the internet. As access of S3 will be provided by the root account so Employees will be able to login and do following steps (There are two steps through console and CLI):

First Go to Amazon S3 > Buckets > Create New bucket. Now you’ll need to fill details which is required on the screen. Like First create Bucket name > choose region (where you want to deploy your workload).

Press enter or click to view image in full size

source : console.aws.amazon.com
Choose Object Ownership (want to make workload Public or private) > Click on ACL enabled >object writer.

Press enter or click to view image in full size

source : console.aws.amazon.com
Allow all public access (tick on acknowledgement) >enabled bucket versioning.

Press enter or click to view image in full size

source : console.aws.amazon.com
Click on create bucket.

Press enter or click to view image in full size

source : console.aws.amazon.com
After Creating S3 bucket we need to change permissions like bucket versioning, data lifecycle and more. Now Bucket is created so let’s upload the file. click on upload > Add files > Destination make sure bucket versioning is enabled > permissions (click on ACL and give public access to make it publicly visible) > Storage Classes (Select from Standard, Intelligent tiering, Standard IA, Glacier >upload You’ll see documents got uploaded.

Note: Standard — Can access on daily basis Intelligent tiering — it’ll track record and charge accordingly Standard IA — Its infrequent Access data which can be accessed once in 6 months Glacier — can be accessed once in a year For Creating Lifecycle rule go to Amazon S3 > Buckets > company — documents > Management > Create lifecycle rules. In that you’ll need to name it and need to decide where you need to apply for whole bucket or single file (I decided whole bucket).

Press enter or click to view image in full size

source : console.aws.amazon.com
Click on move current versions of objects between storage classes > select transition current versions of objects between storage classes (Note you can only go from warm to cold storage classes).

Press enter or click to view image in full size

source : console.aws.amazon.com
Next Review your transition and click on the create rule.

Press enter or click to view image in full size

source : console.aws.amazon.com
CODE IMPLEMENTATION

Now we have two IP (Public and private) address in EC2 Instance so, let’s connect with a secured shell extension for that we need to fill details as shown in below screenshot. In this we need to fill public IP as it’ll be connected to internet.

Press enter or click to view image in full size

Source : SSH Extension
After login in we’ll see that blank SSH screen. If we hit “ls” command we will be able to see that its blank and we don’t have any file in this screen Now we need to first download the keypair as SSH should know where to use it so we’ll be using command “wget keypair” and give permission to use it so we use “chmod 400”.

Press enter or click to view image in full size

Source : SSH Extension
Now we want to go from public IP to private IP so we use private IP to “ssh -i keypair username@ipaddress” and we’ll be able to see that we’re successfully logged in to private IP.

Press enter or click to view image in full size

Source : SSH Extension
As we need to Create Bucket to S3 but before that we need to use some commands to install awscli and for that we’ll be using below commands curl “https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o “awscliv2.zip” unzip awscliv2.zip sudo ./aws/install

Press enter or click to view image in full size

Source : SSH Extension
Before we create bucket, we need to use “aws configure” command to put IAM credentials. In which it’ll ask for following details which we need to fill.

Press enter or click to view image in full size

Source : SSH Extension
Now after CLI is installed we can use aws s3 mb s3://mybucket

we’ll get output: make_bucket: s3://mybucket

Press enter or click to view image in full size

Source : SSH Extension
and bucket is successfully created and you’ll be able to see bucket in S3 with default settings. In case we want to change additional settings, we can go to S3 and change settings.

COST EXPLORER

For Costs we can calculate using simple monthly calculator of AWS but it’ll depend on how we use and which service we use and for how much period of time we can get cost at very granular level such as how much GB of data do we upload and how much time a month will company access it. we also get forecasted cost for future time. To visit cost explorer in AWS console simply go to services > AWS cost management.

Press enter or click to view image in full size

source : console.aws.amazon.com
You can also set your budget for that you have to click on the left-hand side of the screen and click on Budget. There you’ll be able to set Budget on Monthly or daily basis. you can also set a budget amount for your AWS account for All services or for specific services as well. You also get some features like creating Budget Alert where you’ll need to set threshold % (let’s say your budget is 100 USD and you set your threshold to 50% so after your bill reached 50 USD, you’ll get notification).in case you need notification on different email address you can also do that. There are some scenarios where you want to set Budget threshold more than once (Standard practice for AWS is three times 50%,90% and 100%) but you can create as per you convince and lastly, you’ll also need to specify which IAM roles you’re assigning this task. Budget alert helps you to cost optimize your project and The Bill which will be generated every month will be sent to registered email ID of the root account.

RESULTS

As mentioned in introduction we have successfully created 4 unique IDs according to departments and assigned them roles so that they can store documents to s3.

Press enter or click to view image in full size

source : console.aws.amazon.com
We have launched EC2 instances to connect with secured shell with which we can also monitor metrics which will help us to see performance for instances.

Press enter or click to view image in full size

source : console.aws.amazon.com
We use virtual private cloud to secure our instances and workload from unwanted traffic and connected it with EC2.

Press enter or click to view image in full size

source : console.aws.amazon.com
We connected with Command Line Interface and successfully created a bucket so that no other person except the credentials which we inserted in CLI can have access.

Press enter or click to view image in full size

source : console.aws.amazon.com
CONCLUSION

We have Created Unique IDs for different departments so now every department can upload documents securely and they can set different data lifecycle which will prevent them to save cost as when moved from standard to glacier (data is charged in storage for how much number of times the data has been accessed and how much GB has been stored) and we have Also Enabled Bucket Versioning so that if by mistakenly employee has deleted current document so he’ll still be having previous version of that particular document. This is result in smooth and easy process of procurement cycle as before mentioned in Introduction company has to rent a room/lockers to store Important documents of the company so they can store it virtually which will reduce cost and use to restore and backup for Disaster recovery. Incase if company wants, they can also make it public so that everyone can view document. Also, we can set if you want to set your data from Standard to Archive (warm to cold) which will help companies in cost effective way to handle their operational expenses. FUTURE SCOPE Cloud Computing Technology is Already in use by many big firms across including startup companies across the globe but unfortunately in India this technology is used only by big companies and people are unaware of this technology. This technology can be used in each and every company irrespective of their branches or size which will help them to make grow faster. There are many more services that the cloud is launching which help the world to grow at speedy rate. The Most important things which help will help cloud computing to grow in world are:

● Better Cloud Services.

● Security.

● Market Growth.

● Cost-Optimization.

● Virtualization.

REFERENCES

1) console.aws.amazon.com — For Login.

2) Draw.io — For Architecting and Flow chart design.

3) https://docs.aws.amazon.com/s3 — For Simple storage Implementation.

4) https://docs.aws.amazon.com/ec2/ — For Elastic Compute Cloud.

5) https://docs.aws.amazon.com/vpc/ — For Virtual Private Cloud.

6) https://docs.aws.amazon.com/iam/ — For Identity and Access management.

7) https://docs.aws.amazon.com/cli/latest/reference/s3/mb.html — For making bucket commands.

8) https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html — For Installing Aws in CLI to access.

10) https://calculator.s3.amazonaws.com/index.html — Simple Monthly Calculator for Cost Exploration.

11) https://papersowl.com/free-plagiarism-checker — Plagiarism checker website.

Note : This Project is only for reference purpose.
