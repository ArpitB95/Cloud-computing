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




## Launce EC2 from AMI with user data (script)

### APP EC2
- Enter following scrip in user data to automate installing the dependencies

```
#!/bin/bash

sudo apt-get update -y
sudo apt-get upgrade -y

sudo apt install nginx -y
sudo systemctl restart nginx
sudo systemctl enable nginx


sudo apt-get purge nodejs npm
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install npm -y

sudo apt install npm -y
npm install express -y
npm install mongoose -y
```

## DB EC2
- Enter following script in user data to automate downloading of dependencies

```
#!/bin/bash

sudo apt-get update -y

sudo apt-get upgrade -y

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv D68FA50FEA312927

echo "deb https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list

sudo apt-get update -y

sudo apt-get upgrade -y

 sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20 

sudo systemctl restart mongod

sudo systemctl enable  mongod
```

- To check in dependencies are downloaded successfully or not, enter to DB instance and run 'sudo systemctl status  mongod'
- It will show mongod status as active. so it has downloaded successfully.