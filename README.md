## Cloud computing


### Purchasing a Laptop / system
- OS - windows - ubuntu bionic 16.04LTS - Vagrant box online
- Process power
- RAM
- SSD
- Hard drive
- Graphic card
- Power supply
- CPU
- Mother board
- Touch screen 
- Firewall -security tool
- Use - official use , gaming

<img width="670" alt="aws diaa" src="https://user-images.githubusercontent.com/110182832/185413028-a6754e0d-9921-4ffa-bf61-7dbadaa3a5fe.png">


## What is cloud computing ?
- It is a service that use remote servers hosted on the internet to store,​
  Manage and process data​ rather than a local server or personal computer.

- A cloud can be private or public. A public cloud sells services to anyone
  on the internet.
- A private cloud supplies hosted services to a limited number of people, with certain access
 and permissions. Best example of private cloud users is government agencies
- they have their own private cloud for security reasons

- Be it Private or public, the goal of cloud computing is to provide easy, scalable access to computing resources and IT services.

 ## Pros :
- You can access your data from any device and any where in the world as long as you
  have permission to access the data.
- you can easily and instantly deploy servers and can go live in minutes or seconds.
- You can upgrade or downgrade your system as per your requirements.
  let's say traffic on your server increses suddenly than you can upscale and 
  host another servers in minutes which is not possible with on premise server.
- Onother benefit of cloud computing is that pay only for that you used.
  If you've used your ec2 instance for just an hour than pay for that period of time only
  rather than investing in hardware and host it on premise, cloud computing is much cheaper.


## Cons:
- There is possibility of data lost or theft from the data storage, which is very
   rare but can be happen due to natural calamities or in act of war.
- You have limited control over the system and also some time risk to the security.


## 4 Pillars / key benefits of cloud computing
- Ease of use - It's very easy to use and accessible from any device and from anywhere in the world.
-  You can access cloud services from anywhere any time with any device as long as you've permission to access those data.
-  For Ex: Netflix, Monzo

- Flexibility - Cloud computing offers businesses flexibility and scalability when it comes to computing needs.
- Cloud computing allows your employees to be more flexible – both in and out of the workplace. Employees can access files using web-enabled devices such as      smartphones, laptops and notebooks.

- Cost - It has pay as you go model. So you've to pay only for what you've used.

- Robustness - Whether you experience a natural disaster, power failure or other crisis, having your data stored in the cloud ensures it is backed up and protected in a secure and safe location. Being able to access your data again quickly allows you to conduct business as usual, minimising any downtime and loss of productivity.



## AWS Global Infrastructure:



    






- AWS global infrastructure consists of regions and availability zones
- AZs are essentially the physical data centers of AWS. This is where the actual compute, storage, network, and database resources are hosted that we as 
  consumers provision within our Virtual Private Clouds (VPCs).

- As of now, there are total 26 regions across the globe and 84 availability zones that provides amazon web services.
- So, each region can have multiple availability zones and each availability zone has multiple data centers.
- So, let's say if your data is highly important than you can store it to multiple 
  availability zones or to multiple regions. So, something happens to one availability
  zone and whole availability zone goes down the you still have your data safe in another zone. Of course you've to pay for both the zones to store your data.


## Types of cloud services
- Now, there are basically 3 types of cloud services available
- Infrastructure as a service
- platform as a service and software as a service



![types of cloud](https://user-images.githubusercontent.com/110182832/185909059-c81ac2c8-348a-45da-97bf-ccf763242520.png)





- In traditional or on premise services, company has to manage everything from servers, storage, networking, data and security.

- But in Iaas you've to manage only your applications, data, runtime and miidleware.
 - ex iaas: AWS, microsoft azure

 - ex paas: AWS elastic beanstalk, Facebook

 - ex of saas: Gmail, netflix, salesforce
 
 

## Create EC2 instance:
### Here, I've created EC2 instance named app, which has code of app that needs to bee launched.

## Step-1 - Create EC2 instanc on AWS

- Select the Operating system

<img width="950" alt="1" src="https://user-images.githubusercontent.com/110182832/185690198-14ef3b38-79b7-4a92-ad9d-9b5a10cf39e2.png">


## Step -2 - Select the Processing Power

<img width="955" alt="2" src="https://user-images.githubusercontent.com/110182832/185690402-9f7f67f5-650d-4d1a-98ce-df3ca146fa0c.png">


## Step-3 - Congigure instance details

<img width="946" alt="3" src="https://user-images.githubusercontent.com/110182832/185690422-a75d5cf7-34d8-494d-bab4-92e50208e7e6.png">

Change following:
Number of Instance-1
Subnet - Devops student default 1a
Auto assign public id - Enable

## Step-4 - Select the storage

<img width="944" alt="4" src="https://user-images.githubusercontent.com/110182832/185691614-f7eb7264-5a04-4bd4-90e4-f465211ad842.png">



## Step- 5 - Attach tags

- Give name to the instance

<img width="941" alt="5" src="https://user-images.githubusercontent.com/110182832/185691625-4cda2ca7-9536-4051-a0f5-e6c0cebb76dd.png">


## Step-6 - Assign the ports that should be allow to interact with this EC2

<img width="942" alt="6" src="https://user-images.githubusercontent.com/110182832/185691647-be858938-ebb1-481a-b640-8dbc64da4571.png">

- Now, click review and launch.

## To enter the EC2 virtual machine copy Example link shown below and enter in terminal from .ssh folder

<img width="567" alt="7" src="https://user-images.githubusercontent.com/110182832/185692257-080a58bd-9072-4ae5-9536-16e057650acb.png">


<img width="462" alt="8" src="https://user-images.githubusercontent.com/110182832/185692278-215ccf78-2585-4c88-b109-c374d2981d67.png">


## Now Install all the dependencies requiren in app EC2

- Run following commands

````
# update & upgrade ubuntu
sudo apt-get update
sudo apt-get upgrade -y

# nginx install
sudo apt-get install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx

# nodejs install

curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -    # This will download nodejs version 6 or above from website
sudo apt-get install -y nodejs  # Now install nodejs

## Install npm

sudo apt-get install npm

# pm2 install
sudo npm install pm2 -g

````

## Reconfig NGINX which allows reverse proxy ( This means link will work without giving port ex:3000 )
- From home location run 'cd /etc' then 'cd nginx' then 'cd sites-available' then 'sudo nano default'

OR 

' sudo nano /etc/nginx/sites-available/default'

- In default file , under server_name _;
      under location change to 'proxy_pass http://localhost:3000;'
      
      
  <img width="456" alt="9" src="https://user-images.githubusercontent.com/110182832/185694569-7c13248d-3250-4000-8a60-82437210fc84.png">

## Run 'npm install' and 'npm start' and app will be launched


## How to migrate file from local host to Ec2
## With scp command
- 'scp -i [key name] -r [file location in local host] [file destination]
- file destination will be @user:PUBLIC_DNS , so here it will be ubuntu@ec2-34-253-181-132.eu-west-1.compute.amazonaws.com




## Create second EC2 VM - data base EC2

- Follow same steps to create VM
- For security


<img width="863" alt="10" src="https://user-images.githubusercontent.com/110182832/185696231-c6bc5c08-cb97-44fc-aef0-1d382394ce34.png">

## Now Install dependencies in second EC2 (Data base EC2)

````
# update & upgrade ubuntu
sudo apt-get update
sudo apt-get upgrade -y

# retrieve key from mongodb
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv D68FA50FEA312927

# Install required packages
echo "deb https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list

# updates ubuntu
sudo apt-get update
sudo apt-get upgrade -y

# Install mongodb
sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20

# enabl mongodb
sudo systemctl enable mongod

# start mongodb
sudo systemctl restart mongod

````
## Now, config mongod.conf file and change the bind ip to 0.0.0.0
- Navigate from home location to /etc and then to mongod.conf

<img width="352" alt="12" src="https://user-images.githubusercontent.com/110182832/185697209-27561877-30af-4910-bf21-31f7d4ebfeeb.png">

- Change bind IP to 0.0.0.0

<img width="443" alt="11" src="https://user-images.githubusercontent.com/110182832/185697273-2f54c063-8644-4241-8c03-f6f8a9a28d1e.png">

- Now restart mongod by 'sudo systemctl restart mongod'

## Now, set environment variable in app EC2 VM

- From home location run 'sudo nano .bashrc'

<img width="352" alt="12" src="https://user-images.githubusercontent.com/110182832/185699102-9c94750b-0bb3-44ea-8fd1-3a0b396aab48.png">

- Inside .bashrc file, at the end set environment variable called DB_HOST by following command
'export DB_HOST=mongod://give public ipv4 of db ec2/27017/posts'

Here, 'export DB_HOST=mongodb://172.31.26.81:27017/posts'  (172.31.26.81 is private ipv4 of db machine)

<img width="456" alt="13" src="https://user-images.githubusercontent.com/110182832/185699207-302ace58-2cb6-4850-ba9c-f178de048844.png">


- 172.31.26.81:27017/posts is public IPv4 of db VM and 27017 is the port of db EC2

<img width="736" alt="14" src="https://user-images.githubusercontent.com/110182832/185699036-c268bd9f-6df4-47a1-9c8d-954125695412.png">


- Inside app directory goto seeds directory and from inside seeds folder run 'node seed.js'

- Now, from app (where app.js folder is located)
- Run 'npm install' or 'sudo apt-get install npm'
- 'npm install express -y'
- 'npm install mongoose -y'
- 'npm install'
- And 'npm start'

- If full page is not desplayed then go to app/seeds and run 'node seed.js'
- come back to app folder and run 'npm start'


 
 ## Amazon machine image (AMI)
 - An Amazon Machine Image (AMI) is a supported and maintained image provided by AWS that provides the information required to launch an instance.
 - You must specify an AMI when you launch an instance. You can launch multiple instances from a single AMI when you require multiple instances with the same    configuration.

![image](https://user-images.githubusercontent.com/110182832/185997330-6bfc61b4-a953-413b-8401-cc766206ece4.png)



- AMI is created to launch multiple instance from it.
- During the holiday period, it is advisable to run an AMI of an instance as it costs less than actual instance.
- AMI is basically a carbon copy of the instance it created from.


<img width="824" alt="full ami" src="https://user-images.githubusercontent.com/110182832/186005703-9bacd5ac-9050-4117-b078-b3dfa2369614.png">





## Create AMI for app ec2 and db ec2


![ami-1](https://user-images.githubusercontent.com/110182832/186001806-51df1475-9fb3-4325-97b8-43f4f44d5ef4.png)




![bd ami](https://user-images.githubusercontent.com/110182832/186001838-7973eadc-bc65-496f-be1b-166ec3a6a65d.png)





# AWS Disaster Recovery Plan

## AWs DRP is used to secure your data, so something happens to the region or availability zone, still you can access your data.

- For example, here we're storing our data and hosting instances in ireland region.
- In case of unexpected disaster:
- Have an AMI backup
- Store your data to multiple AZs - eu-west-1a,1b,1c
- Second option is to store in multiple region, Ireland as well London
- If whole AWS goes down and data is highly important then have multi cloud deployment in AWS as well Azure or GC
- Hybrid cloud - localhost & public cloud
 

![drp](https://user-images.githubusercontent.com/110182832/186161488-15c96b49-b976-4476-8095-517853051dc9.png)





### To create S3 bucket from CLI, we need python 3.7 above, pip3, aws cli and AWS access and secret key configuration

- ## Setting up AWS keys:
- ## Fisrt download the dependencies:
- sudo apt-get upgrade -y
- alias python=python3

- 'sudo pip3 install awscli'

- ## Configure AWS CLI
- run command 'aws configure'
- enter your access key
- enter your secret access key
- zone- 'eu-west-1'
- 'json'


- ## Create S3 bucket
- ## To run any of the folloeing file 'python file_name'

```
import boto3      # imports boto3 package

s3 = boto3.client('s3')

s3.create_bucket(Bucket = 'eng122-arpit-bucketboto',CreateBucketConfiguration={'LocationConstraint':'eu-west-1'})
```
### OR

```
#!/usr/bin/env python3

import boto3

AWS_REGION = "us-east-2"

resource = boto3.resource("s3", region_name=AWS_REGION)

bucket_name = "hands-on-cloud-demo-bucket"
location = {'LocationConstraint': AWS_REGION}

bucket = resource.create_bucket(
    Bucket=bucket_name,
    CreateBucketConfiguration=location)

print("Amazon S3 bucket has been created")
```



- ## Upload object / file to S3 from EC2 using boto3

```
import boto3

s3 = boto3.client('s3')

s3.upload_file('test.txt','eng122-arpit-bucketboto')   ## ('File_Name', 'Bucket_Name')

```

- ## Download a file from S3 bucket to EC2

```
import boto3

s3=boto3.client('s3')

s3.download_file('eng122-arpit-bucketboto','test.txt','new/test.txt')  #('Bucket_Name', 'Object_Name', 'File_Name')

```


- ## Delete object from S3

```
import boto3

s3 = boto3.client('s3')


s3.delete_object(Bucket='eng122-arpit-bucketboto', Key='object/t1.txt')

```

- ## Delete S3 Bucket

```
import boto3

s3=boto3.client('s3')

s3.delete_bucket(Bucket='eng122-arpit-bucketboto')

```
### OR

```
import boto3

AWS_REGION = "eu-west-1"

resource = boto3.resource("s3", region_name=AWS_REGION)

bucket_name = "eng122-arpit-bucketboto"

s3_bucket = resource.Bucket(bucket_name)
s3_bucket.delete()
```
