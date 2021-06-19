# jenkins-on-aws-ec2 using Amazon Linux AMI instance (Amazon Machine Image)

Setup Jenkins on AWS EC2 instance

#### AWS EC2 Instance - Free Tier specific

```
Navigate to AWS console and sign-in to the AWS account
```
```
Search the service EC2 
```
```
Click on Launch Instance 
```
```
Select Amazon Machine Image - Amazon Linux 2 AMI (HVM), SSD Volume Type
```
```
Select Instance type - t2.micro
```
```
Keep default values - Configure Instance Details
```
```
Can add applicable storage, or keep it as default and click Next
```
```
Add Tag - Name as key => AnyText on Values (ex: Jenkins-EC2-Instance)
```
```
Configure Security Group : We add 3 security group rule for this.
1. SSH type, PORT 22, Source as My IP
2. Custom TCP type, PORT 8080, Source as My IP - This is to access the Jenkin admin on 8080 port on EC2 instance
3. HTTP type, PORT 80, Source as Custom
```
```
Click on Review and Launch, a popup appears , give some name (ex: Jenkins-EC2-key). Select the option to generate the new Key pair, and click on the download.
A new file will be download, keep it for later authenticate with EC2 machine.
```
```
A new EC2 instance can be up and running
Click on the Instance ID, and note down the Public IPv4 address
```



#### SSH into EC2 Instance
```
Open command terminal or git bash
```
```
type the command 
ssh -i <path to the downloaded key file Jenkins-EC2-key.pem> ec2-user@<Public IPv4 address>  (remove angle bracket as well)
```
```
It prompt for confirmation, enter yes. It takes to the EC2 machine, where we can configure Jenkins
```



#### Setup Jenkins on EC2 Instance
```
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key
sudo yum install jenkins -y
sudo yum install java-1.8.0
java -version 
```
```
sudo service jenkins start
The above command starts the Jenkins as a service on EC2 instance. It should give OK running status
```
```
Navigate to the <Public IPv4 address>:8080
Find Public IPv4 address in the EC2 dashboard, under the running instance Id
Jenkins unlock password will prompt first time
Run the command : sudo cat /var/lib/jenkins/secrets/initialAdminPassword
It return some password, copy and paste to the Jenkins panel
```
```
On successfull unlock the Jenkins, it will ask to provide username, password etc. give as your choice, and submit.
It will prompt to install plugins, do click on that. And use the above given username and password to login to Jenkins.
```

