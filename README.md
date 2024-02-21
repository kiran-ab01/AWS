# AWS
https://courses.datacumulus.com/downloads/certified-cloud-practitioner-zb2/ 

**identity access management(IAM)**

-->To access aws we have 3 options:
1.AWS managemnet console(password+MFA)
2.aws command line interface(cli) :protected by access key
3.aws software develpoer kit(sdk): for code-->protected by access key

# EC2 (elastic compute cloud)
capabilities:
vertual machines(vm)
store data on virutal drives(EBS)
distributing load across machines(Elestic load balancer)
scalling usages on auto scalling

**EC2 sizing & configurations**
1.OS: Linux,windows,mac
2.need to chose how much CPU core
3.need to chose RAM
4.how much storage space :
          network attached(EBS&EFS)
          hardware(EC2 instance)
5.network card and speed of the card and pub ip add
6.Firewall rules: security groups

EC2 Instance Types:
![image](https://github.com/kiran-ab01/AWS/assets/132429361/2ddf2be4-8670-495d-b3b3-ed96a4b541b0)
t2 micro is the part of aws free tier

# launch first EC2 instance
1.first we need to add names -> we need to select our OS and also consider arcitecture of OS ->we can select AMI -> instance type like macro, large -> next we need to select key pair to securly connect to our instance.
![image](https://github.com/kiran-ab01/AWS/assets/132429361/2d765653-527b-41e5-a00b-9e4b1643684e)
"store the private key in a secure and accessible location on your computer. You will need it later to connect to your instance"
2. next we need to add network settings.
3. A security group is a set of firewall rules that control the traffic for your instance.
4. also we can enable  https and http , 0.0.0.0/0 allow all IP addresses
4. we can select storage configurations and based on the requiremt and also we get 30 gb in free tir
5. In the user data we can update some commands to run while starting the instance. ex: yum update
6. we can see the details summary based on the selection.

# once the instance is created
we can see
1. instance name 2. instance uniq id 3. public IP addres(what we are going to use to access EC2 instance) 4.private IP addres (which is have to access internally in AWS)
5. AMI ID 6.platform 7.key pair  8.we can get details of security groups(we can configure the port to access)
If we don't want to use we can stop the instance (in the instance state)

If we start and stop the instance Public IP gets changed but private IP will not change.
# EC2 Instance type
![image](https://github.com/kiran-ab01/AWS/assets/132429361/4085df0e-964e-4aec-86dd-62bd244b7f30)
# Security Groups
security groups are fundamental of network security in aws
they control how the traffic is into/ out of our Ec2 
![image](https://github.com/kiran-ab01/AWS/assets/132429361/ac421174-b122-4815-af77-861dc69e6610)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/7dc2aad9-26c9-46f1-b30f-32c6f47eba9f)
If our Application is not accessable (time out) , then its security group issue.
If application gives "connection refused" error , then its an application error/ its not lunched
By defult all Inbound traffic is blocked and outbond traffic is authorized.

Ports to know:
![image](https://github.com/kiran-ab01/AWS/assets/132429361/43db8c71-c28f-48a5-b725-42da3f5dcdc5)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/05b7e578-18bb-4cdd-8c93-5321a270544a)


# to connect through ssh in linux and mac
we need to place .pem file which is downloded in to the specific folder and need to run **SSH ec2-user@publicIP**
By defult intsnace create ec2-user to access so we need to make use of that.
If we get an error like : too many authentication failure : Thats becouse we have not specified the key which is downloded.
To sepecify go to the path to .pem file and use **ssh -i filename.pem ec2-user@publicIP** 

after this if we face another error like: unprotected private key , we need to give permisstion like: **chmod 0400 filename.pem** 



