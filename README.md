# VOL-7-LAB: S3 Permanent Mount on EC2 using s3fs

# Step 1: Create S3 Bucket

Go to Amazon Web Services Console

Open Amazon S3

Click Create bucket
Enter:

Bucket name: my-bucket-alfia (must be unique)

Region: same as EC2

Keep default settings → Click Create bucket

Upload File

Open bucket → Click Upload

Upload a file (example: index.html)

# Step 2: Create IAM Role for EC2

Go to AWS Identity and Access Management

Click Roles → Create role

Select:
Trusted entity: AWS Service

Use case: EC2

Attach policy:
AmazonS3FullAccess

Role name: EC2-S3-Access

Click Create role

# Step 3: Launch EC2 Instance

Go to Amazon EC2

Click Launch instance

Configure:
Name: S3-Mount-Server

AMI: Ubuntu

Instance type: t2.micro

Key pair: create/select

Network: Default VPC

Auto-assign Public IP: Enable

Security Group:

Allow:
SSH (Port 22) → Anywhere (0.0.0.0/0)

Click Launch instance

# Step 4: Attach IAM Role to EC2

Select instance

Go to:
Actions → Security → Modify IAM Role

Select:
EC2-S3-Access

Click Update IAM Role

# Step 5: Connect to EC2

ssh -i your-key.pem ubuntu@<public-ip>

# Step 6: Install s3fs and Dependencies

sudo apt update

sudo apt install -y s3fs


If needed (for full dependency support):

sudo apt install -y automake libfuse-dev gcc libcurl4-openssl-dev libxml2-dev make libssl-dev

# Step 7: Create Mount Directory

sudo mkdir /data

cd /data

# Step 8: Mount S3 Bucket

sudo s3fs my-bucket-alfia /data -o iam_role=auto

What this does:

my-bucket-alfia → your S3 bucket
/data → mount point

iam_role=auto → uses EC2 IAM role (no keys needed)

# Step 9: Verify Mount
cd /data

ls


You should see:

index.html


That confirms your S3 bucket is mounted successfully.

# Step 10: Test Sync

Create file from EC2:

echo "Hello from EC2" > test.txt

Now check in S3 bucket → test.txt will appear.

# Step 11: Permanent Mount (Auto Mount on Reboot)

Edit fstab:

sudo nano /etc/fstab


Add this line:

s3fs#my-bucket-alfia /data fuse _netdev,iam_role=auto 0 0


Save and exit.

Apply:
sudo mount -a

Final Result

What this really means is:

Your S3 bucket behaves like a local folder
Any file added in EC2 → appears in S3
Any file uploaded in S3 → appears in EC2
Mount remains even after reboot














# VOL-7-LAB-S3-PERMANENT-MOUNT

CREATE S3 BUCKET-- create

upload object 

create role in iam 
roles
aws service - ec2- s3 full acess policy
name --- create 

create ec2 instance
ami
key pair 
t2.micro 
network default 
public eanble 
ssh 22 
lainch 

# connect instance

make directory

mkdir /data

cd /data

attach iam role attach too

go to instance

select server

action --- security -- modify iam role

select s3 full acesss-- update iam role

# using ubuntu

```bash
sudo apt update
```
```bash
sudo apt install -y s3fs
``` 
```bash
sudo apt install -y automake libfuse-dev gcc libcurl4-openssl-dev libxml2-dev make libssl-dev
```



connect to ec2

sudo su 

cd /data

mount using ths command
```bash
s3fs <bucket-name> /mountpoint -o iam_role=auto
```

```bash
s3fs my-bucket /mnt/s3 -o iam_role=auto
```
 
go to s3 upload object
 go to instance check in mount points 
```bash 
 cd /data
```
```bash
 ls
```
  we can see index.html file 
















action --- security -- modify iam role

select s3 full acesss-- update iam role



