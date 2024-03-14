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
# to connect through ssh using windows below window-10
we need to make use of free ssh claint plugin called putty.
First we need to save our private key, so open putty gen and serch for the .pem file and save it .
we need to convert pem file to ppk format to access in putty.
need to give public ip and port number to access.if we face any issues just give ec2-user@publicip and port number to login.
To add private key in catogory --> connection --> ssh --> auth --> browse for ppk file stored in local.

# to connect through window above window-10
we can connect through ssh method in CMD / we can make use of putty.
![image](https://github.com/kiran-ab01/AWS/assets/132429361/b8baa095-f01e-4b08-86f8-4dea8b851a64)

we can connect Ec-2 instance using ec2 terminals.
# Iam roles
never ever enter our scurity access keys into an ec2 instance/ terminals becouse any one can able to login using our accounts.
insted we can make use of IAM rolse attached to ec2 instance in security to provide the credentials.

# Ec2 Instance storage sections
![image](https://github.com/kiran-ab01/AWS/assets/132429361/06c27969-6669-4173-8613-ad395271d56a)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/d3850664-afca-4d64-b355-49bde1f08909)

# EBS volumes attched to ec2 instance
go to ec2 instance -> storage -> under that we can find volume -> we can create new EBS volume.
after that its not attched to any instance -> to attach -> click on action -> attach volume -> select instance -> click on attach volume.
Note: if we have diffrent Zone compare to ec2 instance and EBS volume we can't able to attche the instance.it should be same.

If we are going to terminate the ec2 instance.In EBS volume-> ec2 storage section -> **delete on termination** should be **No** becouse if we terminate the ec2 instance EBS volume also terminated if we select the defult option.
# EBS Snapshots
make a backup->snapshot of our EBS volum at any point of time.
![image](https://github.com/kiran-ab01/AWS/assets/132429361/ddb8a91a-89d6-4cdf-bbf4-512a62ee48ce)
we can move EBS snapshot to archive tier which is cheeper.
we can recycle bin for deleted snapshots/ we can set retention ruls to accidental deleted snapshots from1 day to year.
to take a snapshot -> go to EBS volume -> actins -> create snapshots-> we can give description -> click on create snapshots.
we can copy snapshot to other region ans also by takeing this snapshot we can recreate the volume -> go to snapshot -> click on action -> create volume from snapshot -> and select region.
# AMI = Amazon machine image 
ami are a custamization of an EC2 instance.
![image](https://github.com/kiran-ab01/AWS/assets/132429361/25d482f6-0071-44d6-b2c8-08f7dffa8302)
To create AMI -> go to ec2 instance -> right click on instance -> image and templets -> create image -> image name -> create image.
in the left side under AMIS -> Images -> we can see the AMI images -> once the AMI images are avilable we can create instance using those images / by creating a instance only we can select ami images shared by/owned by.
AMI snapshot will also take a backup in customizable way.

# Ec2 image builder
![image](https://github.com/kiran-ab01/AWS/assets/132429361/5b516c41-a29a-47c9-b0e8-051b063ef689)
image builder is free serveice only it will cost for resource like ec2 instannce creation, ami storage, etc.
# EFS = elastic file system
![image](https://github.com/kiran-ab01/AWS/assets/132429361/07130215-7862-4f5a-8b61-cce2d29896a1)

# EBS v/s EFS
![image](https://github.com/kiran-ab01/AWS/assets/132429361/6be78f9f-47a7-4ecc-a81b-14f4d9ced3da)
# EFS-IA
![image](https://github.com/kiran-ab01/AWS/assets/132429361/47223d25-e8d7-46aa-9b80-b1bf2c220467)

# Elastic load balancing
Scalabilty & high availablity
scalablity: application/system can handle greate loads and in scalabilty we have vertical scalabilty and horizantal scalablity.
vertical scalabilty: incressing the size of the instance.ex: t2.micro to t2.large.
horizantal scalablity: incress the no of instance/system for your application.:ex: multiple operators can constanty work if one os not avaialble also.
**high availablity**: running our application/system in at least 2 avialablity zone.ex: is we have some issue in availablity zone 1 the avaiablitty zone 2 need to run.ex:multiple nodes.
# Load balancing 
![image](https://github.com/kiran-ab01/AWS/assets/132429361/c4045f7b-515f-4e3c-b773-885d01148d6d)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/b8765ffa-9661-48fc-b270-5dff51baa3b0)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/f2165d5b-8c68-47b9-ae7c-fd49ba1fb9a7)

First ready 2 instance -> under load balancing -> load balancers-> create load balanecr-> we get 3 LB and select application load balencer-> give name ->scheme is internal-facing ->Ip address type is IPv4 -> in network mapping we need to select availablity zone ->select security group(add inbound and outbond ruls) -> (need to create target group -> we have to rigister a target) -> create load balencer.
Through the target group is going to send the trafic.

# Auto scaling group
![image](https://github.com/kiran-ab01/AWS/assets/132429361/20183ea2-19ef-4bfb-b9af-f9d031e804b8)
To create atou scalling group -> under atou scaling ->atou scaling group -> give name-> we need to create launc templ(in this tmpt we can say how to create ec2 instance. ex:we can select os, Ami,instnace type,security group, etc) -> we can select network where we can select availablity zone for atou scling group -> next -> next we need to select load balnecer -> select attche to an existing load balancer -> select LB -> next -> configure group size and scling policy -> select desired capacity(how many instance we want at any time) -> minimu capacity(1 atlest need ) and maximum capacity(4 maximum we may required 4 instance)->next -> create auto scaling group.
after creating a atou scalling group the new 2 ec2 instance will be created as we mentiond in the desired capacity.
The target group in the load balaning also pointing to the new instance created.
**Note: If we terminate one of the ec2 instance, becouse of in atou scalling group we decide as 2 desired capacity it will create a new instance.if any sinatce is unhealty new instance will created becouse of atou scalling for replacement** 
![image](https://github.com/kiran-ab01/AWS/assets/132429361/1d1352e5-f996-408d-875c-2c4c1b0b8399)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/f35f5aad-94c3-43ce-bbac-f0f6cd047406)

# Amazon S3
Amazon s3 is used for backup and storage,disastor recovery,archive,hybrid cloud storage,application hosting,media hosting.
amazon s3 allow people to stores data/file in bucket(directories)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/325f6aef-28e5-4fc7-b309-2ba0c6c6b50f)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/2ab220e0-4dbe-448e-9ac9-5fb76ff23f0b)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/eebbb5ce-8cb4-4dba-94cb-7fa0991010c8)
To create s3 bucket-> give bucket name -> aws region ->we can chose copy setting from privious bucket ->create bucket.
to update objects to the bucket -> click on upload ->add files -> select files -> upload.
we can create folder in the s3 bucket and also we can upload files.

# amazon s3 security
json based policy,
How to attache s3 bucket policy ->bucket-> permisstion -> block public access setting(by defult public permisstion is blocked if we enable to public access our data can be access to any user in the internet) ->bucket policy -> we can write a json based policy.
if we don't know how to write a policy we have aws polic generator: https://awspolicygen.s3.amazonaws.com/policygen.html (it will generate a policy for us based on the requirement).

# s3 versioning 
![image](https://github.com/kiran-ab01/AWS/assets/132429361/268ed6f7-dd08-4981-93ab-f04321d6567e)

# s3 replication 
![image](https://github.com/kiran-ab01/AWS/assets/132429361/207200e5-94d5-44aa-a0b8-5bb9b5cadb16)

# RDS(relatinal database) in aws
in services -> Rds-> database-> create database -> select standard/easy -> select engine -> select like mysql,postgres,oracle,etc -> select version -> select templte->db name->give master username->master password->select storage type(ssd,)->select allocated storage->enable storage atouscalling->select vpc & vpc security group->database ports->done.

after creation-> in connectivity & security we get endpoint to connect and port details. in monitering we get CPU utilization/db connection details and also storgage space .
we can also take snapshot of the database and we can also restore the snapshot databse(it create new database),we can copy the database diff regin,share the database to another aws account.
![image](https://github.com/kiran-ab01/AWS/assets/132429361/e8fd06cb-a29a-4227-9a61-9055aa75eadf)
create dynamodb-> go to dynamodb -> table -> create table->table names->sepcify partition key-> create table(in table we can add values, we can't link table to table).
similarly we have multiple datbase supported in aws : https://bluexp.netapp.com/blog/aws-cvo-blg-aws-databases-the-power-of-purpose-built-database-engines
# database migration service
![image](https://github.com/kiran-ab01/AWS/assets/132429361/1c243d19-e1ab-4694-9f2d-a49400d71c16)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/4b6578c8-70fc-4708-80a6-80b4c5de75f7)

# aws lambda
![image](https://github.com/kiran-ab01/AWS/assets/132429361/567ef89f-05fb-4df3-9796-fe8246b2f0de)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/66fbb4c5-b1f2-43de-814d-a3a67b0af18b)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/4fd8ea22-9b02-4b32-a58c-4b8f0ffaa310)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/701af2a0-ab32-4b61-912c-f0ac74f850c5)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/933a027c-5a9a-47be-b2a3-896f807135ab)

# AWS cloud formation
infrastructre as code in the cloud formation ex:terraform
![image](https://github.com/kiran-ab01/AWS/assets/132429361/7db0c49b-02d5-4324-830f-40a9171f16b1)
cloud formation will give atomatic infrastructure creation when we have code/old infrastructure.(create in us-east(n.vergina) regin)
cloud formation->create->select templet->we can upload ymal files or url(in ymal files they should be  code to create instance/any other configuration)->give name ->done
we can get desgin view after we attached the templet.

# Beanstalk
PAAS->platfrm as a service
to add beanstalk service-> create->select tier->give application name-> select platform type->chose application code/we can upload our code-> select presets(single instance/high avilablity)->select service roles->we can select more configuration.

# amazon route 53
![image](https://github.com/kiran-ab01/AWS/assets/132429361/3d4e684f-ec25-4fc9-9132-a41b57fe743e)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/b2301da8-f63e-4c0b-808c-881882f125f1)
Route 53-> to get started with route 53 we need to rigister domine(it will cost).to rigiester a domin(go to route 53->rigister domine ->give domine-> and select availble one->done
In the hosted zone we are going to place the dns records.
Now to add route 53-> go to the hosted zone->create records->give record name->ex:www.(kiran.com- domine which rigisterd) ->in the value give public ip->and in routeing policy->select latancy-it will access to users which is near to them(we have diffrent type of route ex:simple,weighted,failover,etc)->select regin->we can add another record for other ec2-instance-done.

if we open a new tab and serach www.kiran.com in google it will locate to the ec2-inastance that is closest to user. and if we use the vpn and serch the url it will navigate to there instnace.

# cloudwatch 
where we can get the alert notification if cpu utilization is high/some of the reports.
cloudwatch-> all matrix->we may see multiple-we can configure how we needed.

# VPC-virutual private cloud
IP -> public ip,private ip,elastic ip.
![image](https://github.com/kiran-ab01/AWS/assets/132429361/a516af68-1bbf-4e04-b6ad-4bda2c103708)
 Internet gateway:helps vpc to connect with the internet.
If we have any instance in private subnet and that need to connect with internet, if we need to give accesable to internet for that we need to have **NAT gateway**that nat gatway will connect with internet gateway.
![image](https://github.com/kiran-ab01/AWS/assets/132429361/8718fc00-f78e-45df-a6e8-647f62a8aea1)
by default after aws account is created 1 vpc,3subnets,1routetable,1internet gatway,1 networkacls,1security groups.
![image](https://github.com/kiran-ab01/AWS/assets/132429361/9e59ce4a-a167-424e-893c-fbba4b1a6394)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/41f76ffc-e831-4b18-9c37-bf0fb6120b5f)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/914266f9-c83d-4d12-9fb7-318c8ad90611)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/1c4fa4ce-4564-455c-916f-174b7f44562e)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/4fc4ba3a-ed02-418c-b2d5-8019762c3e8d)
![image](https://github.com/kiran-ab01/AWS/assets/132429361/17fecf73-d609-45f3-8e44-927232d87ffe)







