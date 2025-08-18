Launch Ubuntu EC2 Instance(Ubuntu)

Install Required Packages
  - apt-get update 
  - apt install openjdk-11-jdk
  - apt install git 
  - apt install maven 

Add Jenkins Repository and Key
  - curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
  - echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

Install Jenkins
  - apt install jenkins

Start and Enable Jenkins also check status
  - sudo systemctl start jenkins
  - sudo systemctl enable jenkins
  - systemctl status jenkins

Allow port 8080 in ec2 instance security group

Access Jenkins:
  - http://your-ec2-public-ip:8080

Get Jenkins Admin Password
  - cat /var/jenkins_home/secrets/initialAdminPassword

Install Suggested Plugins & Create Admin User
  - After unlocking, Jenkins will ask you to install plugins.
  - Choose "Install suggested plugins"
  - Then set up your first admin user

Configure Maven in Jenkins
  - Go to: Manage Jenkins → Global Tool Configuration
  - Under Maven:
      - Add Maven
      - Name: Maven_3.8.6
      - Check "Install automatically"

Create a Freestyle Job
  - New Item → Freestyle Project → Name: "your project name"
  - Source Code Management: Git
      - Repo URL: "your github repo"
  - Build Section:
      - Add build step → Invoke top-level Maven targets
      - Goals: clean package
      - Maven Version: Maven_3.8.6

Create jenkins file.
  - Go to Jenkins → New Item → Pipeline
  - Name: HelloMavenPipeline
  - Under Pipeline Definition:
      - Select Pipeline script from SCM
      - SCM: Git
      - Repo URL: "your github repo"
      - Script Path: Jenkinsfile
