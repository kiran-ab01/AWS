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
2. next we need to add network settings 



