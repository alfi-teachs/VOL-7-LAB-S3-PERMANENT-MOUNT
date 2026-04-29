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



