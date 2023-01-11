### 1. What is CI/CD? What are the available tools to implement CI/CD?
CI/CD (Continuous Integration and Continuous Deployment/Delivery) is a set of practices that enable teams to build, test, and release software faster and more frequently.
1. Continuous Integration (CI) is a development practice where developers regularly integrate their code into a shared repository. Each integration is then verified by an automated build and test process. By integrating regularly, teams can detect and fix errors quickly, and avoid the "integration hell" that can happen when several developers work on the same codebase without frequent integrations.
2. Continuous Deployment (CD) is an extension of Continuous Integration that automatically deploys the application to a production environment after the code has passed the automated tests. This allows teams to deliver new features and bug fixes to customers quickly and safely.

There are many tools available to implement CI/CD, some of the most popular ones include:
1. Jenkins: An open-source CI/CD tool that is widely used for automating builds, tests, and deployments.
2. Travis CI: A hosted, distributed CI/CD service that supports many programming languages including Java, Ruby, Python, and Go.
3. CircleCI: A cloud-based CI/CD platform that supports a wide range of programming languages and platforms.
4. GitLab CI/CD: A built-in feature of GitLab that allows you to create, manage, and run CI/CD pipelines within the GitLab application.
5. Azure DevOps: A set of services offered by Microsoft that includes a CI/CD service that can be integrated with other services such as version control and work item tracking.
6. AWS CodeBuild, CodeDeploy and CodePipeline: Set of tools offered by Amazon web services to handle different aspect of CI/CD process.
7. Bamboo : A popular CI/CD tool by Atlassian that offers a wide range of integration options and support for multiple languages.

### 2. What are the stages in CI-CD?
The stages in a CI/CD pipeline typically include:
1. Code Development: Developers write and commit code changes to a version control system such as Git.
2. Build and Test: The changes are built and tested automatically using tools such as Jenkins or Travis CI.
3. Integration: The changes are integrated with the main branch of the codebase.
4. Deployment: The changes are deployed to a staging environment for further testing.
5. Release: The changes are released to the production environment after they have been thoroughly tested and approved.
6. Monitoring : The application performance and user experience is tracked in the production environment and any issues are identified, resolved and fixed.

### 3. What are the stages in CI-CD pipeline?
1. Code Commit: Developers write code and commit changes to a version control system such as Git.
2. Build: The changes are built automatically using tools such as Jenkins, Travis CI, CircleCI, Gitlab-CI.
3. Test: Automated tests are run to ensure that the changes haven't introduced any new bugs and that the application still functions as expected. This include unit tests, integration tests, acceptance tests and other types of tests.
4. Deployment: The changes are deployed to a staging environment for further testing.
5. Release: The changes are released to the production environment after they have been thoroughly tested and approved.
6. Monitoring: The application performance and user experience is tracked in the production environment and any issues are identified, resolved and fixed.

### 4. What are the steps in CI-CD pipeline?
Continuous Integration (CI)
1. Continuous Download: The process of frequently pulling the latest code from a version control repository (such as git) and preparing it for building and testing.
2. Build: The process of compiling the code and creating executable artifacts (such as JAR or WAR files).
3. Test: Automated tests, such as unit tests and integration tests, are run against the newly built code to ensure that it is functional and does not break any existing functionality.
Continuous Deployment (CD)
1. Staging: The process of deploying the code to a pre-production environment, where it can be further tested and validated before release to production.
2. Release: The process of deploying the code to the production environment, where it is made available to end-users.
3. Monitor: The process of monitoring the application and infrastructure in production, to ensure that they are working as expected and to identify and resolve any issues that may arise.

### 5. Elaborate the stages in CI-CD pipeline?
1. Continuous Download: Developers create some code and upload that code into the version controlling system.The moment code is uplaoded CI/CD tool(ex: Jenkins) gets a notification and it will download that code. This step is called Continuous Download.
2. Continuous Build: The code downloaded in the previous stage has to converted into an artifact. This artifact can come in the format of war,jar,ear,exe file etc.To convert the code into an artifact jenkins takes the help of centain build tools like
ANT,Maven,MsBuild etc.
3. Continuous Deployment: The artifact created in the previous stage is now deployed into the testing environment. This Testing environment can be running on some application servers like tomcat,Jboss,Weblogic etc.Jenkins should deploy the artifact into
these application servers from where testers can start accessing it.
4. Continuous Testing: Jenkins now executes the automation test scripts created by the testers and check if the application is working according to the clients requirement. If it doesn't, Jenkins will send email notifications to the concerned team members and developers will fix the defects and upload the modified code into the version controlling system.Jenkins will now start from stage 1.
5. Continuous Delivery: If testing passes Jenkins will now take approvals from the delivery team and deploy the artifact into the prod environment where the end user can start accessing it.
6. Continous Monitoring:?

### 5. Setup Sample CI/CD using Jenkins, QA and Prod Servers.
1. Setup of Jenkins \
a. Create 3 AWS "ubuntu 20" instances \
b. Name the first one as Jenkins second as QAServer and third as ProdServer \
c. Connect to Jenkins AWS instances using git bash \
d. Update the apt repository 
```
  sudo apt-get update
``` \
e. Install jdk
```
  sudo apt-get install -y openjdk-8-jdk 
``` \
f. Install git and maven
```
  sudo apt-get install -y git maven
``` \
g. Download jenkins.war
```
  wget https://get.jenkins.io/war-stable/2.249.1/jenkins.war
```  \
h. To start jenkins
```
  java -jar jenkins.war
``` \
i. To access jenkins from a browser
```
  https://public_ip_of_jenkinserver:8080
``` \
j. Unlock Jenkins by entering the admin password
k. Click on "Install Suggested plugins"
l. Create first admin user
m. Click on Continue--->Finish--->Save

2. Setup of QA and ProdServers
a. Connect to QAServer AWS instance using git bash
b. Update the apt repository
```
  sudo apt-get update
```
c. Install tomcat9
```
  sudo apt-get install -y tomcat9
```
d. Install tomcat9-admin
```
  sudo apt-get install -y tomcat9-admin
```
e. Edit the tomcat-users.xml file
```
  sudo vim /etc/tomcat9/tomcat-users.xml 
```
f. Delete the entore content of the file and add the below data
```
  <tomcat-users>
     <user username="nswamyg" password="221222" roles="manager-script"/>
  </tomcat-users>
```
g. Restart tocmat9
```
  sudo service tomcay9 restart
```
h. To access tomcat from browser
```
  https://public_ip_of_qa:8080
```

3. Repeat the above g steps on ProdServer AWS instance
a. To access tomcat from browser
```
  https://public_ip_of_prod:8080
```

### 5. Graphical Setup of CI/CD in Jenkis
1. Continuous Download:
a. Open the dashboard of Jenkins
b. Click on New item
c. enter item name as "Development"
d. Select Free Style Project--->OK
e. Go to Source Code Management
f. Select Git
g. Enter the github url where Developers have uplaoded the code
  https://github.com/[user]/[repository].git
h. Click on Apply--->Save
i. Go to the dashboard of Jenkins
j. Go to the Development job--->click on Build icon

This job will download all the code created by the developers

2. Continuious Build:
a. Open the dashboard of Jenkins
b. Go the Development job---->Click on Configure
c. Go to Build section
d. Click on Add Build step
e. Click on Invoke top level maven targets
f. Enter the Goal:    package
g. Click on Apply---->Save
h. Go to the dashboard of Jenkins
j. Go to the Devlopment job--->click on Build icon

This job will create an artifact from the downloaded java code.

3. Continuous Deployment:
a. Open the dashboard of Jenkins
b. Click on Manage Jenkins
c. Click on Manage Plugins
d. Go to Available section
e. Search for "Deploy to Container" plugin
f. Click on Install without restart
g. Go to the dashboard of Jenkins
h. Go to the Development job--->Click on configure
i. Go to Post Build actions
j. Click on Add Post build action
k. Click on Deploy war/ear to container
l. war/ear file: **/*.war\
   context path: testapp\
   Click on Add container---->Select tomcat9\
   Enter tomcat9 credentials\
   Tomcat url: private_ip_of_QAServer:8080\
m. Apply---->Save\

This job will deploy the artifact into the QAServer and to access the application from the browser using public_ip_of_qaserver:8080/testapp

4. Continuous Testing
a. Open the dashboard of Jenkins
b. Click on New item--->Enter item name as Testing
c. Select Free Style Project---->OK
d. Go to Source Code Management
e. Select Git
f. Enter the giturl where testers have uploaded the selenium test scripts \
  https://github.com/intelliqittrainings/FunctionalTesting.git \
g. Go to Build section
h. Click on Add Buil step
i. Click on Execute shell\
  java -jar path_Testingjar/testing.jar \
j. Apply--->Save
k. Go to the dashboard of JEnkins--->Go to Testing job--->Click on Build icon

This job will download all the Selenium test scripts and execute them on the application deployed into the QAServer.

5. Linking Development job to Testing job
Development job should be linked with the Testing job so that after all the stages in the Development job it will trigger the Testing job.

a. Open the dashoboard of Jenkins
b. Go to Development job--->Click on configure
c. Go to Post Build actions
d. Click on Add Post Build actions
e. Click on Buil other projects
f. Enter project name as "Testing"
8. Apply---->Save

6. Copying artifacts from Development job and Testing job
a. Open the dashboard of Jenkins
b. Click on Manage Jenkins--->Manage Plugins
c. Go to Available section
d. Search for "Copy Artifact" plugin
e. Click on Install without restart
f. Go to the dashboard of Jenkins
g. Go to the Development job--->Click on configure
h. Go to Post Build actions
i. Click on Add Post Build actions
j. Click on Archive the artifacts \ 
   File to archive: **\*.war  \
k. Apply--->Save
l. Go to the dashbord of Jenkins
m. Go to the Testing job---->Click on Configure
n. Go to Build section
o. Click on Add Build step
p. Click on Copy artifacts from other projects
q. enter project name as Development
r. Save

7.Continuous Delivery
a. Open the dashboard of JEnkins
b. Go to the Testing job
c. Click on Configure
d. Go to Post Build actions
e. Click on Add post build action
f. Click on Deploy war/ear to container
g. war/ear files: **/*.war \
  Context path: prodapp \
  Click on Add container \
  Select tomcat9 \
  Enter username and password of tomcat9 \
  Tomcat url: private_ip_of_prodserver:8080 \
h. Apply--->Save

=========================================================================
Day 5
=========================================================================
Alternate ways of Setup of Jenkins
==============================================
1 Update the apt reposiotry and install java
  sudo apt-get update
  sudo apt-get install -y openjdk-8-jdk

2 Add the jenkins repository key to the apt repository
  wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key 
                                                     | sudo apt-key add -

3 Add the debain repository address to jenkins.list file
  sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > 
                                     /etc/apt/sources.list.d/jenkins.list'

4 Update the apt repository
  sudo apt-get update

5 Install jenkins
  sudo apt-get install -y jenkins

========================================================================
Setup of Jenkins on tomcat
==============================
1 Update the apt repository
  sudo apt-get update

2 Install tomcat9 and tomcat9-admin
  sudo apt-get install -y tomcat9 tomcat9-admin

3 Download the jenkins.war
  wget https://get.jenkins.io/war-stable/2.249.1/jenkins.war

4 Give wirite permisssions to other on tomcat9 folder
  sudo chmod o+w -R /var/lib/tomcat9

5 Copy this war into jenkins
  cp jenkins.war /var/lib/tomcat9/webapps

6 To access tomcat from browser
  public_ip:8080
  To access jenkins
  public_ip:8080/jenkins

====================================================================
User Administration in Jenkins
===========================================

Creating users in Jenkins
===========================
1 Open the dashboard of jenkins
2 click on manage jenkins
3 click on manage users
4 click on create users
5 enter user credentials

Creating roles and assgning
==============================
1 Open the dashboard of jenkins
2 click on manage jenkins
3 click on manage plugins
4 click on role based authorization strategy plugin
5 install it
6 go to dashboard-->manage jenkins
7 click on configure global security
8 check enable security checkbox
9 go to authorization section-->click on role based strategy  radio button
10 apply-->save
11 go to dashboard of jenkins
12 click on manage jenkins
13 click on manage and assign roles
14 click on mange roles
15 go to global roles and create a role "employee"
16 for this employee in overall give read access
   and in view section give all access
17 go to project roles-->Give the role as developer
   and patter as Dev.* (ie developer role can access
   only those jobs whose name start with Dev)
18 similarly create another role as tester and assign the pattern as "Test.*"
19 give all permissions to developrs and tester
20 apply--save
21 click on assign roles
22 go to global roles and add user1 and user2 
23 check user1 and user2 as employees
24 go to item roles
25 add user1 and user2
26 check user1 as developer and user2 as tester
27 apply-->save
If we login into jenkins as user1 we can access only the development 
related jobs and user2 can access only the testing related jobs


===========================================================================
Day 6
===========================================================================
MAster Slave Architecture of Jenkins
============================================
This is used distribute the work load to additional linux
servers called as slaves.This is used when we want to run multiple 
jobs on jenkins parallelly.

Setup
============
1 Create a new AWS ubuntu20 instance

2 Install the same version of java as present in the master
  sudo apt-get update
  sudo apt-get install -y openjdk-8-jdk

3 Setup passwordless SSH betwen Master and slave
  a) Connect to slave and set password to default user
     sudo passwd ubuntu
  b) Edit the ssh config file
     sudo vim /etc/ssh/sshd_config
     Search for "PasswordAuthentication" and change it from no to yes
  c) Restart ssh
     sudo service ssh restart
  d) Connect to Master using git bash
  e) Generate the ssh keys
     ssh-keygen
  f) Copy the ssh keys
     ssh-copy-id ubuntu@private_ip_of_slave
     This will copy the content of the public keys to a file called
     "authorised_keys" on the slave machine

===========================================================================
Day 7
===========================================================================
  Connect to slave using git bash
4 Downlaod the slave.jar file
  wget http://private_ip_of_jenkinsserver:8080/jnlpJars/slave.jar

5 Give execute permissions to the slave.jar
  chmod u+x slave.jar

6 Create an empty folder that will be the workspace of jenkins
  mkdir workspace

7 Open the dashboard of Jenkins
  
8 Click on Manage Jenkins--->Click on Manage Nodes and Clouds

9 Click on New node---->Enter some node name as Slave1

10 Select Permanant Agent--->OK

12 Enter remote root directory as /home/ubuntu/workspace

13 Labels: myslave (This label is associated with a job in jenkins
   and then that job will run on that slave)

14 Go to Launch Method and select "Launch agent via execution of command on master"

15 Click on Save

16 Go to the dashboard of Jenkins

17 Go to the job that we want to run on slave---->Click on Configure

18 Go to General section

19 Check restrict where this project can be run

20 Enter slave label as myslave

=============================================================================
Day 7
=============================================================================
=====================================================================
Pipeline as Code
======================
Implementing all the stages of CI-CD from the level of a Grrovy script
file is called as Pipleine as Code.This groovy script files is called
as Jenkinsfile and generally it is uploaded into the remote git server
along with the application code.From the remote git server this JEnkinsfile
will trigger all the stages of CI-CD

Advantages
====================
1 Since the stages of CI-CD are implemented from the level of code
  it can perform version controlling on it ie it gives the team members
  ability to edit and review the code and yet maintain multiple versions 
  of jenkinsfile

2 Jenkinsfile can withstand planned and unplanned restarts of the Jenkins
  master

3 It can perform all stages of CI-CD with minumum number of plugins as
  a result of which it give better perfromance than the free style projects

4 It can handle all the real time challanges like if conditions,
  errror handling etc


Pipeline can be implemented in 2 ways
1 Scripted Pipeline
2 Declarative Pipeline

Syntax of Scripted Pipeline
=================================
node('master')
{
   stage('Stage name in CI-CD')
   {
       Groovy script code for implementing this stage
   }
}


Syntax of Declarative Pipeline
====================================
pipeline
{
   agent any
   stages
   {
      stage('Stage name in CI-CD')
      {
          steps
          {
               Groovy script for implementing this stage
          }
      }
   }
}

============================================================================
Scripted Pipeline Code
==========================
node('master') 
{
    stage('ContinuousDownload_Master') 
    {
         git 'https://github.com/intelliqittrainings/maven.git'
    }
     stage('ContinuousBuild_Master') 
    {
        sh label: '', script: 'mvn package'
    }
    stage('ContinuousDeployment_Master')
    {
        sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.55.129:/var/lib/tomcat8/webapps/qaapp.war'
    }
    stage('ContinuousTesting_Master')
    {
        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
        sh label: '', script: 'java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline/testing.jar'
    }
     stage('ContinuousDelivery_Master')
    {
       
        sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.48.61:/var/lib/tomcat8/webapps/prodapp.war'
    }
    
    
    
    
    
}
=====================================================================
Day 8
=====================================================================
In most cases the jenkinsfile is uploaded into the github
along with the application code by the developers.The jnekinsfile
for the remote gitserver will  trigger all the stages of ci-cd

Developers Activity
===========================
1 Clone the maven project 
  git clone https://github.com/intelliqittrainings/maven.git

2 Move into this cloned repository and delete the .git folder
  cd maven
  rm -rf .git

3 Create a new git repo and send the code into the stagging area and local
  repository
  git init
  git add .
  git commit -m "a"

4 Create a file called Jenkinsfile and copy paste the Scripted pipeline
  code.

5 Send it to stagging and local reposiotry
  git add .
  git commit -m "b"

4 Open github.com---->Signin into you account

5 Click on + on top right corner---->Click on New repository

6 Enter some reposiotry name--->Select Public or Private
  Click on Create repository

7 Go to Push an existing reposiotry from command line
  Copy and paste the first command.This will create a link between the
  local reposiotry and the remote github repository

8 Copy the second command
  git push -u origin master

Devops Enginers Activity
==============================
1 Open the dashboard of Jenkins

2 Click on New item--->Enter some itemname

3 Select Pipeline project--->OK

4 Go to Pileline section--->Select Pipeline script from SCM

5 Select SCM as Git

6 In Repository url: Enter the github url where we uploaded the code

7 Click on Apply--->Save

============================================================================
Declarative Pipeline
==============================================================================
Declarative Pipeline
------------------------
pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
               sh label: '', script: 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
               sh label: '', script: '''
scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.45.245:/var/lib/tomcat8/webapps/newtestapp.war'''
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh label: '', script: 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                input submitter: 'srinivas', message: 'Waiting for Approval!'
                
                 sh label: '', script: '''
scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.42.87:/var/lib/tomcat8/webapps/newprodapp.war'''
            }
        }
    }
}

========================================================================
Declarative Pipeline with Post Conditions
-----------------------------------------------

pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
               sh label: '', script: 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
               sh label: '', script: '''
scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.45.245:/var/lib/tomcat8/webapps/newtestapp.war'''
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh label: '', script: 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
    }
    post
    {
        success
        {
            input submitter: 'srinivas', message: 'Waiting for Approval!'
                
                 sh label: '', script: '''
scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.42.87:/var/lib/tomcat8/webapps/newprodapp.war'''   
        }
        failure
        {
            mail bcc: '', body: 'Continuous Integration has failed so unable to proceed with Delivery', cc: '', from: '', replyTo: '', subject: 'CI Failed', to: 'gandham.saikrishna@gmail.com'
        }
    
    
    }
    
    
    
    
    }
================================================================================

CatLight Notifications
==============================
This is a client side s/w which is used to send notifications
of jenkins jobs in the form of simple pop msgs
Cat light has to be installed on every individual team 
members machines

1 Open https://catlight.io/downloads
2 Download and install catlight for windows
3 Open cat light and it will display the list of CI tools that it can connect to
3 Select JEnkins
4 Enter the public_ip_of_jenkins_Server:8080
  Enter username and password of jenkins
5 Catlight will display the list of jobs available in jenkins
6 Select the jobs for which we need notifications
7 Run that job in Jenkins and we will get a desktop notification

============================================================================
Day 9
============================================================================
Exception Handling in Declarative Pipeline
=================================================================
pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                script
                {
                   try
                   {
                       git 'https://github.com/intelliqittrainings/maven.git'
                   }
                   catch(Exception e1)
                   {
                       mail bcc: '', body: 'Jenkins is unable to download from remote github', cc: '', from: '', replyTo: '', subject: 'Download failed', to: 'gitadmin@outlook.com'
                       exit(1)
                   }
                }
               
            }
        }
         stage('ContinuousBuild')
        {
            steps
            {
                script
                {
                   try
                   {
                       sh label: '', script: 'mvn package'
                   }
                   catch(Exception e2)
                   {
                       mail bcc: '', body: 'Jenkins is unable to create an artifact from the code', cc: '', from: '', replyTo: '', subject: 'Build failed', to: 'developers@outlook.com'
                      exit(1)
                   }
                }
               
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                script
                {
                   try
                   {
                      sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.31.15:/var/lib/tomcat8/webapps/testwebapp.war'
                   }
                   catch(Exception e3)
                   {
                       mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the QaServers', cc: '', from: '', replyTo: '', subject: 'Deployment failed', to: 'middleware@outlook.com'
                       exit(1)
                   }
                }
                
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                script
                {
                                    
                    try
                    {
                        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                       sh label: '', script: 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
                    }
                    catch(Exception e4)
                    {
                       mail bcc: '', body: 'Functional testing of the app on QAServers failed', cc: '', from: '', replyTo: '', subject: 'Testing failed', to: 'testers@outlook.com'
                       exit(1)
                    }
                }
                
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                script
                {
                   try
                   { 
                        input message: 'Waiting for Approval!', submitter: 'naresh'
                        sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.26.41:/var/lib/tomcat8/webapps/prodwebapp.war' 
                    }
                    catch(Exception e5)
                    {
                         mail bcc: '', body: 'Unable to deploy into ProdServers', cc: '', from: '', replyTo: '', subject: 'Delivery failed', to: 'delevery@outlook.com'
                    }
                }
            }
        }
       
    }
  
       
}

=================================================================
Exception handling in Scripted Pipeline
=================================================================
node('master') 
{
    stage('ContinuousDownload') 
    {
        script
        {
            try
            {
                 git 'https://github.com/intelliqittrainings/maven.git'
            }
            catch(Exception e1)
            {
                 mail bcc: '', body: 'Jenkins is unable to download the code from the git repository', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'gitadmin@gmail.com'
                       exit(1)
            }
        }
       
    }
    stage('ContinuousBuild')
    {
        script
        {
            try
            {
                sh 'mvn package'
            }
            catch(Exception e2)
            {
                 mail bcc: '', body: 'Jenkins is unable to create an artifact from the code', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'devlopers@gmail.com' 
                      exit(1)
            }
        }
        
    }
    stage('ContinuousDeployment')
    {
        script
        {
            try
            {
                 sh 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.16.229:/var/lib/tomcat9/webapps/testapp.war'
            }
            catch(Exception e3)
            {
                 mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the QAServers', cc: '', from: '', replyTo: '', subject: 'Deployment Failed', to: 'middleware.team@gmail.com'
                        exit(1)
            }
        }
        
        
    }
    stage('ContinuousTesting')
    {
        script
        {
            try
            {
                 git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                 sh 'java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline/testing.jar'
            }
            catch(Exception e4)
            {
                mail bcc: '', body: 'Functional Testing of the selenium scripts has failed', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'testers.team@gmail.com'
                        exit(1)
            }
        }
      
    }
    stage('ContinuousDelivery')
    {
        script
        {
            try
            {
                input message: 'Waiting for Approval from DM!', submitter: 'srinivas'
         sh 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.29.16:/var/lib/tomcat9/webapps/prodapp.war'
            }
            catch(Exception e5)
            {
                mail bcc: '', body: 'Delivery into the prod servers has failed', cc: '', from: '', replyTo: '', subject: 'Delivery Failed', to: 'delivery.team@gmail.com'
            }
        }
        
    }
    
    
    
    
    
}
=======================================================================
Webhooks 
===========
This is  used to send notifications from github to jenkins
Whenever any code changes are done and that is checkdin into
github, webhook will send an immediate notifiction ot JEnkins
and Jenkins will triggern the job

1 Open github.com---->Click on the reposiotry that we are working on
2 On the right corner clikc on Setting
3 Click on Webhooks in the left pannel
4 Click on Add Webhook
5 In Payload URL: http://public_ip_jenkinsserver:8080/github-webhook/
6 In Content type select :application/json
7 Click on Add Webhook
8 Open the dashboaard of Jenkins
9 Go to the job that we want to configure
10 Go to Build triggers
11 Check GitHub hook trigger for GITScm polling
12 Click on Apply--->Save
   Now if we make any changes to the code in github then github
  will send an notification to jenkins and jenkins will run that job


==============================================================================
Day 10
==============================================================================

MultiBranch Pipeline
===========================
Developers upload multiple functionalities code on different branches
On each of these branches there will be a copy of the Jenkinsfile
which has CI instructions of what should be done on that branch

Developers Activity
=========================
1 Clone the maven repository
  git clone https://github.com/intelliqittrainings/maven.git

2 Move into this cloned repository and delete .git folder
  cd maven
  rm -rf .git

3 Initilise a new git repository
  git init

4 Send the files into stagging area and local repository
  git add .
  git commit -m "a"

5 Create a jenkins file and put the stages of CI that should happen 
  on master  branch
  vim Jenkinsfile

6 Send it to stagging and local repository
  git add .
  git commit -m "b"

7 Create a new branch called loans and create a create a new Jenkinsfile
  git checkout -b loans
  vim Jenkinsfile
  Use the CI instructions that should be done on Loans branch

8 Send this to stagging and local repoistory
  git add .
  git commit -m "c"

9 Open github.com---->Create a new repository

10 Push all the branches from local machine to remote github
   git push origin --all

Jenkins Admin Activity
==============================
1 Open the dashboard of Jenkins

2 Click on New item---->Enter item name as MultBranchPipeline

3 Select MultiBranchPipeline--->OK

4 Go to Branch Sounrces---->Select Git-->enter github url where developers
  uploaded the code

5 Go to Scan Multi branch pipeline triggers---->Select 1 minute

6 Apply--->Save


 










































 





 




























































 













































































