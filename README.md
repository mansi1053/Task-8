Launch Ubuntu EC2 Instance(Ubuntu)

Install Required Packages
  - apt-get update 
  - apt install openjdk-11-jdk
  - apt install git 
  - apt install docker.io

Enable Docker and add your user:
  - systemctl start docker
  - systemctl enable docker
  - usermod -aG docker ubuntu

Run Jenkins via Docker:
docker run -d \
  --name jenkins \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts

Get Jenkins Admin Password
  - docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword

Allow port 8080 in ec2 instance  security group

Access Jenkins:
  - http://your-ec2-public-ip:8080

Create JAVA Maven App
Add to GitHub repo

Configure Maven in Jenkins
  - Go to: Manage Jenkins → Global Tool Configuration
  - Under Maven:
      - Add Maven
      - Name: Maven_3.8.6
      - Check "Install automatically"

Create a Freestyle Job
  - New Item → Freestyle Project → Name: HelloMaven
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
