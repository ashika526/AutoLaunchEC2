# AutoLaunchEC2

This yaml template allows you to launch a new AWS EC2 instance in the default VPC with a new security group using ansible playbook. 

Prerequisites: 
1) AWS Free Tier Account and little knowledge on where abouts of EC2
2) Python,pip,ansible and boto installed on EC2 linux instance(preferebly)
3) Access key id and secret key credentials of the user 

Procedure:
I will split this entire procedure of deployment of EC2 instance into parts.

Step1: IAM User Credentials
1) Create an IAM user and make sure that you have given programmatic and console access to that user. 
2) Make sure to save the credentials locally in your desktop.

Step2: Launching EC2 Host instance through GUI
1) Sign in into AWS Management console 
2) Search for EC2 service in services and launch a new EC2 Linux instance with instance type t2.micro in the default VPC. 
3)You can select a new security group or you can choose an existing security group(its your wish). Open SSH Port 22 in inbound rules and just keep everything default and proceed to next steps for launching an instance. 
4) If you have a key pair already then you can use it otherwise generate a new key.
5) After successfull launching, login as a root into your instance using any software like PUTTY, MOBAXTERM, Ubunutu 18.0.4 (I use Ubunutu 18.0.4)
Command to login using ssh:  ssh -i "YourKeyName.pem" ec2-user@PublicDNS(IPv4)
If you are using PUTTY make sure that you convert .pem to .ppk otherwise save your key.pem file in your local directory and change the permissions to 400 and ssh into your EC2 instance. If you are unsure about this procedure, you can just click on your instance -> go to connect option -> you will find the procedure to connect into your instance.


Step3: Installations on your host EC2
1) Now we should install ansible on our host EC2. But ansible requires python and pip. So, follow the below commands to install the required:
  i) yum install python
  ii) yum install pip
  iii) pip install ansible
  iv) pip install boto and pip install boto3
2) Check if everything is perfectly installed or not by seeing the versions of python,pip,ansible and boto

Step4: Save the credentials into .boto file
1) Now, as everything is installed goto root directory and make a file named boto and make sure that its a hidden file. Because those are our keys and they must be confidential. 
2) Save your access key id and access secret key in that file. For your reference see file (boto)
3) Make sure that you save the file in root folder only. 

Step5: Create an inventory file in /etc/ansible
1) Now goo to /opt directory and make a folder called ansible
2) Change the directory to ansible and make a file named hosts which contains your target environments (I have used local host). For your reference see (hosts) file.

Step5: Create and run ansible playbook
1) Now you can make a directory in your home directory and create a yml file which contains code to deploy a new EC2 instance. 
2) Create ansible playbook using : vi yourfilename.yml . For your reference see (createec2.yml) file
3) Check your ansible playbook for any errors including syntax using command ansible-playboook -i yourinventoryfilename youransibleplaybookfile --check
4) If everything is ok, then run the playbook using command ansible-playbook -i yourinventoryfilename youransibleplaybook.

Step6: Check for successfull deployment
Now signinto your management console and check if the ip address displayed in your output is matching the public ip address displayed on the GUI . 

If the instance is successfully deployed and running with out any errors then Congratualations!!!

You have successfully automated the procedure of deploying EC2 instance using Ansible Playbook. 

  
  
  
  
  
  
  
  
  
