Group No : 04
										Online Book Store

Siddharth Devare - 21104136
Siddhi Desale    - 21104135
Praniv Warungshe - 21104031
Harsh Jikambde   - 21104073

	This application tries to create an essence of an online book store via a simple yet powerful medium and stimulates the working of an online book store.
 
EXP1- To understand the benefits of Cloud Infrastructure and Setup AWS Cloud9 IDE, Launch AWS Cloud9 IDE and Perform Collaboration Demonstration.

1)Login to AWS management console
Navigate to Cloud9 -> Create Environment
Give Name ->
Environment type(New EC2 instance)
Instance type (t2.micro)
Platform (Amazon Linux 2)
Timeout (30 minutes)
everything else keep as it is.
CREATE 
It will take few minutes to create aws instance for your Cloud 9 Enviornment.

2)Till that time open AWS management console in New tab
Navigate to IAM
Create User->give user name
tick (Provide user access to the AWS Management Console)
tick ( I want to create an IAM user)
select custom password and CREATE A PASSWORD(note down your password)
untick (Users must create a new password at next sign-in)
NEXT
Select Add user to group
Click on Create Group
Give User Group name
Click on Create User Group
NEXT
CREATE USER

3)Now close that window and Navigate to USER GROUPS from left pane in IAM.

click on your group name which you have created and navigate to permission tab

Now click on Add permission and select Attach Policy after that search for Cloud9 related policy and select Awscloud9EnviornmentMember policy and add it.

Now click on your user group and then click on add user and add user you have created. 

4)Go to the Previous Cloud9 Tab and click on OPEN(CLOUD9 page will open)
click on file-> new from template->HTML file
Write the Title in the html file and SAVE it(some content)
Now click on Share Button at top right corner, put the IAM user name that you have created and enable persmission as RW click on INVITE, then DONE
Click OK for Security warning.

5)Now Open your Browsers Incognito Window and login with IAM user which you configured before.
Give the ACCOUNT ID (you can find it on the AWS managent console by clicking on the [YOURNAME]dropdown at top right corner)
and enter the IAM username and password that you gave while creating IAM user

6)After Successful login with IAM user open Cloud9 service from dashboard services and click on shared with you enviornment to collaborate.

7)Click on Open IDE you will same interface as your other member have to collaborate in real time, also you all within team can do group chats



EXP2- To Build Your Application using AWS CodeBuild and Deploy on S3 / SEBS using AWS CodePipeline, deploy Sample Application on EC2 instance using AWS CodeDeploy.

1)  Login to AWS management console
2)  Create S3 Bucket->give name(other all keep default)-> create bucket
3)  Create Second S3 Bucket-> give name->untick(block all public access)-> tick (I acknowledge that the current settings might result in this bucket and the objects within becoming public.)->keep other setting as it is->create bucket
4)  Create CodeBuild Project->give name->Select Source Provider(GITHUB)->Select Repository in my Github Account-> Repository URL ( https://github.com/Sankalp2808/Car-pwa-deploy-on-aws.git )->In Environment->Select Operating System(Amazon Linux 2)->Runtime(standard)->Image (aws/codebuild/amazonlinux2-x86_64-standard:5.0)->
Image version (Always use the latest image for this runtime version)-> Environment type(Linux)-> Select New Service Role ->Role Name(Appears automatically, dont change)-> BuildSpec -> select use a buildspec file ->Artifacts -> type(No artifacts) ->Logs ( tick Cloudwatch Logs)-> Create Build Project
5)  Create CodePipeline ->give name->Advanced Settings->Select Custom Location-> Bucket dropdown (Select Bucket 1) -> NEXT -> Source Provider (Github version 1)-> Click connect to github->Confirm -> Repository(Car-pwa-deploy-on-aws)-> Branch(master)-> Change detection option (Github webhooks)-> NEXT -> Build Provider (AWS CodeBuild) -> Select your Project Name ->NEXT-> Deploy Provider (Amazon S3)-> Bucket Dropdown (Select Bucket 2)-> TICK (Extract file before deploy)->NEXT->CREATE PIPELINE
6)  Build Will be Failed
7)  Click on View in CodeBuild(View in CodeBuild is above view logs button where the BUILD FAILED is shown)
8)  After Redirecting ->click on Build details->scroll down(Environment)->click on the service role link given
9)  After IAM page in opened in new tab-> click on your ROLE name->click on add permissions-> ADD AmazonS3FullAccess -> check in the permissions if it is added(permissions tab of your role)
10)  Go To CodePipeline -> click on your pipeline -> retry the failed stage (it will succeed in few minutes)
11)  Go to S3-> click on bucket2-> p-> scroll down to Static Website Hosting (edit)-> Select Enable->Index Document(index.html)->Save Changes
12)  on the page which appears click on permissions->Bucket Policy(edit)->paste this code(remember to put your bucket2 name in code) -> 
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::Bucket-Name/*"
            ]
        }
    ]
}

SAVE CHANGES
13)  on the page which appears after saving the code -> click on Properties->Scroll to last of page(Static Website Hosting)->click on the link given in that section->website is opened



EXP3- Install and spin up a kubernetes cluster on Linux Machines / Cloud Platforms
1)Login to AWS 
2)Use N.Virginia region for free tier account
3) Search EC2 Service
4)Check Security groups
   Except Default â€“delete all other security group if exit
5)Go to EC2 -> Launch Instance -> number of instances(in right panel) -> 2 ->  Name: Master 
6)Select Ubuntu in Quick start
7)CLICK ON CREATE NEW KEY PAIR -> name: kp -> create key pair 
8)Firewall security group -> create security group -> check allow SSH traffic from ->check allow HTTPs traffic from the internet -> Allow HTTP traffic from the internet -> Anywhere 
9)Click on Launch Instance.Once both the instances are created change the name of the second instance to Slave
10)Click on Master -> Connect -> Connect
11)Click on Slave -> Connect -> Connect
12)Assign Unique Hostname for Each Server Node -> 
 Mater ->  sudo hostnamectl set-hostname master-node
 Slave -> sudo hostnamectl set-hostname worker-node-01
13)Steps to Install Kubernetes should be executed on both Master and Slave Terminals
Set up Docker
i-Install Docker
Kubernetes requires an existing Docker installation.
sudo apt-get update
Next, install Docker with the command:
sudo apt-get install docker.io
Repeat the process on both master and slave that will act as a node.
Check the installation (and version) by entering the following:
docker - -version
ii-Start and Enable Docker
Set Docker to launch at boot by entering the following:
sudo systemctl enable docker
sudo systemctl status docker
sudo systemctl start docker
iii-Install Kubernetes
Add Kubernetes Signing Key
(https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)
Follow the steps from this link which will also be provided by maâ€™am
Steps in Link if maâ€™am doesn't give:
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl



EXP4- To install Kubectl and execute Kubectl commands to manage the Kubernetes cluster and deploy Your First Kubernetes Application.
EXECUTE ALL THE COMMANDS OF EXP 3
Kubernetes Deployment: 
sudo swapoff â€“a (on both master and slave)
Initialize Kubernetes on Master Node not on slave 
sudo kubeadm init --pod-network-cidr=10.244.0.0/16--ignore-preflight-errors=all




EXP5- To understand terraform lifecycle, core concepts/terminologies and install it on a Linux Machine.
cd Documents/<your file>/
1)wget -O- https://apt.releases.hashicorp.com/gpg
2)sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
3)echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
4)sudo tee /etc/apt/sources.list.d/hashicorp.list
5)sudo apt update && sudo apt install terraform
6)unzip terraform_1.6.2_linux_amd64.zip ( if not working then ls and enter correct file name)
7)sudo mv terraform /usr/local/bin/
8)terraform --version



EXP6- To build,change and destroy AWS infrastructure using terraform
1)follow the steps of exp5
2)sudo apt-get install curl
3)curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
4)sudo apt-install unzip
5)sudo unzip awscliv2.zip
6)sudo ./aws/install
7)aws --version
8)open browser and log in to aws>click on profile>security credentials>scroll down create access key>check the check box>copy both the keys in a notepad file>done
make sure region is global
9)go back on terminal and type
aws configure
add your access key
add your secret access key 
default region name: us-east-1 
default output format keep it blank by pressing enter
10)cd ~
mkdir project-terraform
cd project-terraform
11)again go to aws>ec2>launch instance>
name:myFirstInstance <make sure to keep this name only as its the same name in config files>
ubuntu image
t2.micro instance type 
create a new key pair 
name of keypair is terraform
.pem file 
click on create keypair
and launch instance
12)create terraform files on terminal type
sudo nano variables.tf
in that file type
variable "aws_region" {
   description = "The AWS region to create things in."
   default = "us-east-1"
}

variable "key_name" {
   description = "SSH keys to connect to ec2 instance"
   default = "terraform"
}

variable "instance_type" {
   description = "instance type for ec2"
   default = "t2.micro"
}

save and close
13)go back on aws>instances>click on the instance you created>scroll down and in details tab you will find ami id copy that and paste in the notepad file
14)go back on terminal and type here note: in this line you have to make changes as ami = "ami-0b9064170e32bde34" put your ami id 
sudo nano main.tf
in this file type 
provider "aws" {
  region = var.aws_region
}

# Create security group with firewall rules 
resource "aws_security_group" "security_jenkins_port" {
  name        = "security_jenkins_port"
  description = "security group for jenkins"

  ingress {
    from_port   = 8080
    to_port     = 8080
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  # outbound from Jenkins server
  egress {
    from_port   = 0
    to_port     = 65535
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "security_jenkins_port"
  }
}

resource "aws_instance" "myFirstInstance" {
  ami           = "ami-0b9064170e32bde34"
  key_name      = var.key_name
  instance_type = var.instance_type
  security_groups = [aws_security_group.security_jenkins_port.name]
  
  tags = {
    Name = "jenkins_instance"
  }
}


save the file and close
15)terraform init
16)terraform plan
17)terraform apply
enter a value: yes 
wait till execution is complete might take a while
18)go to aws>refresh your instances pages
jenkins_instance will be created automatically because of terraform
19)terraform destroy
20)go to aws>refresh your instances pages
jenkins_instance will be terminated automatically because of terraform destroy
21)delete instances, key pair and everything experiment is complete 



EXP7- To understand the Static Analysis SAST process and learn to integrate Jenkins SAST to SonarQube/GitLab. 
1)Install jenkins 
i- sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
or
sudo wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
Ii- sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
iii- sudo apt update
iv- sudo apt install jenkins 
V- sudo systemctl start jenkins
Vi- sudo systemctl status jenkins
Vii-sudo ufw allow 8080
Viii- open browser localhost:8080, You should see the Unlock Jenkins screen
ix- In the terminal window, use the cat command to display the password:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Copy the 32-character alphanumeric password from the terminal and paste it into the Administrator password field, then click Continue.
x-Install suggested plugins>next>create user 
Xi- in case there is a user and you dont have password
cd /var/lib/jenkins/ 
nano config.xml
Initial security something make it false
Save and close 
service jenkins restart
Open browser and restart

2)Install sonarqube 
docker run -d -p 9000:9000 sonarqube
In browser go to localhost:9000

3) initial login
Username: admin
Password: admin 
Create new password and login to sonarqube

4)go to my account by clicking on profile photo>security>generate token
Name: token1 
Type: global analysis token
Expires: in 30 days 
Then generate >copy token id and paste it somewhere 

5)Open jenkins in browser>manage jenkins>plugins>available plugins>
Sonarqube scanner>install and click on restart jenkins 
6)go to manage jenkins>system>scroll down sonarqube server
Click on add sonarqube
Name: sonarqubeserver
url:http://locahost:9000
Apply and save 

7) go to manage jenkins>tools>scroll down sonarqube scanner installation
Add sonarqube scanner
Name:sonarqubescanner
Click on install automatically
Or install from maven central and highest version
Apply and save

8)go to dashboard >new item>pipeline project
Name: Sonarqubepipe
Desc: this is sonarqube pipeline
Check github project box
Add github url â€œhttps://github.com/vishal003/jenkins-sonarqubeâ€
Scroll down select pipeline script add this in textbox
node
{
    stage('clonning from GIT'){
git branch: 'main', credentialsId:'GIT_REPO', url:'https://github.com/vishal003/jenkins-sonarqube.git'
    }
}
Apply and save



EXP8- Create a Jenkins CICD Pipeline with SonarQube / GitLab Integration to perform a static analysis of the code to detect bugs, code smells, and security vulnerabilities on a sample Java application.
1)follow steps of exp7
2)change the pipeline script to script given by maam if not given
node
{
    stage('clonning from GIT'){
git branch: 'main', credentialsId: 'GIT_REPO', url: 'https://github.com/vishal003/jenkins-sonarqube.git'
    }
    
stage('SonarQube Analysis') {
    def scannerHome = tool 'SonarQube'
        withSonarQubeEnv('SonarQube'){
        sh """/var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/SonarQube/bin/sonar-scanner \
        -D sonar.projectVersion = 1.0-SNAPSHOT \
            -D sonar.login=admin \
        -D sonar.password=India@011 \
        -D sonar.projectBaseDir=/var/lib/jenkins/workspace/sonarqube \
            -D sonar.projectKey=my.app1 \
            -D sonar.sourceEncoding=UTF-8 \
            -D sonar.language=java \
            -D sonar.sources=project/src/main/java \
            -D sonar.tests=project/src/test/java \
            -D sonar.host.url=â€http://127.0.0.1:9000/"""
            }
}
}
3)go to dashboard>manage jenkins>plugins>available plugin>
Install blueocean 




EXP9- To Understand Continuous monitoring and Installation and configuration of Nagios Core, Nagios Plugins and NRPE (Nagios Remote Plugin Executor) on Linux Machine
1)sudo apt-get update
2)sudo apt-get install wget build-essential unzip openssl libssl-dev
3)sudo apt-get install apache2 php libapache2-mod-php php-gd libgd-dev
4)cd ..
5)cd /opt/
6)sudo wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.3.tar.gz 7)sudo tar xzf nagios-4.4.3.tar.gz
8)cd nagios-4.4.3
9)sudo ./configure --with-command-group=nagcmd
10)sudo make all
11)sudo make install 
12)sudo make install-init 
13)sudo make install-daemoninit
14)sudo make install-config 
If you show execution till here it's okay as we have not created a nagios user so the other steps cannot be executed 



EXP10- SKIP

EXP11- To understand AWS Lambda, its workflow, various functions and create your
first Lambda functions using Python / Java / Nodejs.
1) check server > n. Virginia
2) services search for lambda (under compute section)
3) create function 
	Author from scratch
	Function name = sum
	Runtime = Python
	Architecture = x86_64
	Change deafult execution role ( dropdown ) > Create a new role with basic Lambda permissions
  ---Take ss---
4) create function
  ---Take ss--- 
 now scroll down to code source and edit lambda_funciton.py add this code:

import json

def lambda_handler(event, context):
	first_number = 100
	second_number = 200
	sum = first_number + second_number 
	return sum
 ---Take ss---
5) now click on drop down of test button > configuration test event
	test event action : create new event 
	Event Name : hello-world
	Event sharing settings : private
	template : hello-world ( by default, it is taken form Event Name)
	Event JSON:
{

}
(put these empty brackets)
---Take ss---
	save

6)Click on the Deploy button beside to the test button > now click on Test button > Execution result sub tab will open :
(EXPECTED OUTPUT)
	Test Event Name :
		hello-world
	Response
		300
---Take SS---
7) Now create another lambda function 
	services > lambda > create function
	Author from scratch
	Function name = name
	Runtime = Python
	Architecture = x86_64
	Change default execution role ( dropdown ) > Create a new role with basic Lambda permissions
---Take SS---
8) now scroll down to code source and edit lambda_funciton.py add this code: 
def lambda_handler (event, context):
	if event["name"] == "Soham": (replace your name)
	 return "apsit"(make sure the indentation is correct as its a python file)

9) click on the dropdown of the test button > Configure test event
Test event action > Create new event 
	Event name : name
	Event sharing settings : Private
	Template : hello-world (by default or maybe the same if you changed previously)
	Event JSON:
{
   "name": "soham"
      }
(Change it to your name)
---Take ss---
save

10) Click on Deploy > button beside to test after that click on the test button 
	Execution result (OUTPUT):
	Test Event Name
	name

	Response
	"soham"
---Take ss---

	

EXP12-To create a Lambda function which will log â€œAn Image has been addedâ€ once you add an object to a specific bucket in S3
1) check server > n. Virginia
2)services search for S3(under compute storage)
3)Create bucket 
	Bucketname : adlsucks (Change the name)
	AWS Region : US east (n. virginia)us-east-1
--take ss--
	create bucket 
4)Service search for IAM (under compute storage Security, Identity, & Compliance)
	Leftside dashboard > Access management > Roles
	Create Role:
		Trusted entity type: AWS service
		Use Case : Lambda
		permissions : AmazonS3FullAccess, AWSLambda_FullAccess and CloudWatchFullAccess (click on checkboxes)
		Next
		Role name : Sohamrole
  ----Take SS of role name , role description , permissions ---
		create role

5)services search for lambda (under compute section)
Create Function :
	Author from scratch
	Function name : lambdatrigger
	runtime : node.js
	architecture : x86_64
	Change default execution role(dropdown) : Use an existing role > dropdown will appear >select Sohamrole (or role name you gave)
	---Take ss---
	create function

6) Function overview > add trigger
	Select a source : S3
	Bucket : adlsucks (or the bucket you created)
	Event types : All object create events (selected by default)
	Suffix : .jpg  (keep prefix empty)
	tick the I acknowledge check box 
	---take ss---
7) scroll down and open the code tab :
index.mjs:
exports.handler = function(event, context, callback){
    console.log('incoming event: ',event);
    const bucket = event.Records[0].s3.bucket.name;
    const filename = decodeURIComponent(event.Records[0].s3.object.key.replace(/\+/g, ' '));
    const message = `An image has been added - ${bucket} -> ${filename}`;
    console.log(message);
    callback(null,message);
    
};

click on deploy > test :
	Test event action : Create new event
	Event name : exp12
	Event sharing settings: Private
	Template : exp12
	Event JSON :
{

}
(in event json these brackets are suppose to be empty)
8) go to s3 bucket and select your bucket -> click on add file -> and now add a .jpg image from your computer or just download a .jpg image from browser. -> upload.
9) Go to cloudwatch ->Logs -> log groups -> select any one stream and take the ss of the logs 


EXP13- SKIP 
