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

### 5. Ca you elaborate the stages in CI-CD pipeline?
1. Continuous Download: Developers create some code and upload that code into the version controlling system.The moment code is uplaoded CI/CD tool(ex: Jenkins) gets a notification and it will download that code. This step is called Continuous Download.
2. Continuous Build: The code downloaded in the previous stage has to converted into an artifact. This artifact can come in the format of war,jar,ear,exe file etc.To convert the code into an artifact jenkins takes the help of centain build tools like
ANT,Maven,MsBuild etc.
3. Continuous Deployment: The artifact created in the previous stage is now deployed into the testing environment. This Testing environment can be running on some application servers like tomcat,Jboss,Weblogic etc.Jenkins should deploy the artifact into
these application servers from where testers can start accessing it.
4. Continuous Testing: Jenkins now executes the automation test scripts created by the testers and check if the application is working according to the clients requirement. If it doesn't, Jenkins will send email notifications to the concerned team members and developers will fix the defects and upload the modified code into the version controlling system.Jenkins will now start from stage 1.
5. Continuous Delivery: If testing passes Jenkins will now take approvals from the delivery team and deploy the artifact into the prod environment where the end user can start accessing it.
6. Continuous monitoring:  The process of constantly monitoring the various stages of the software development lifecycle, such as code development, testing, and deployment. This allows teams to quickly identify and address any issues that arise, ensuring that the software is of high quality and ready for release. It also helps in tracking the performance of the software, and identifying potential bottlenecks or security vulnerabilities.

### 5. How to setup CI/CD using Jenkins, QA and Prod Servers in AWS?
1. **Setup of Jenkins** 
- Create 3 AWS "ubuntu 20" instances 
- Name the first one as Jenkins second as QAServer and third as ProdServer 
- Connect to Jenkins AWS instances using git bash 
- Update the apt repository 
```
  sudo apt-get update
```
- Install jdk
```
  sudo apt-get install -y openjdk-8-jdk
```
- Install git and maven
```
  sudo apt-get install -y git maven
```
- Download jenkins.war
```
  wget https://get.jenkins.io/war-stable/2.249.1/jenkins.war
```
- To start jenkins
```
  java -jar jenkins.war
```
- To access jenkins from a browser
```
  https://public_ip_of_jenkinserver:8080
```
- Unlock Jenkins by entering the admin password
- Click on "Install Suggested plugins"
- Create first admin user
- Click on Continue--->Finish--->Save

2. **Setup of QA and ProdServers**
- Connect to QAServer AWS instance using git bash
- Update the apt repository
```
  sudo apt-get update
```
- Install tomcat9
```
  sudo apt-get install -y tomcat9
```
- Install tomcat9-admin
```
  sudo apt-get install -y tomcat9-admin
```
- Edit the tomcat-users.xml file
```
  sudo vim /etc/tomcat9/tomcat-users.xml 
```
- Delete the entore content of the file and add the below data
```
  <tomcat-users>
     <user username="nswamyg" password="221222" roles="manager-script"/>
  </tomcat-users>
```
- Restart tomcat9
```
  sudo service tomcat restart
```
- To access tomcat from browser
```
  https://public_ip_of_qa:8080
```
- To access tomcat from browser
```
  https://public_ip_of_prod:8080
```

### 6. How to setup CI/CD pipeline in jenkins free style project?
1. **Continuous Download:**
- Open the dashboard of Jenkins
- Click on New item
- enter item name as "Development"
- Select Free Style Project--->OK
- Go to Source Code Management
- Select Git
- Enter the github url where Developers have uplaoded the code
  ```
   https://github.com/[user]/[repository].git  
  ```
- Click on Apply--->Save
- Go to the dashboard of Jenkins
- Go to the Development job--->click on Build icon

This job will download all the code created by the developers

2. **Continuious Build:**
- Open the dashboard of Jenkins
- Go the Development job---->Click on Configure
- Go to Build section
- Click on Add Build step
- Click on Invoke top level maven targets
- Enter the Goal:    package
- Click on Apply---->Save
- Go to the dashboard of Jenkins
- Go to the Devlopment job--->click on Build icon

This job will create an artifact from the downloaded java code.

3. **Continuous Deployment:**
- Open the dashboard of Jenkins
- Click on Manage Jenkins
- Click on Manage Plugins
- Go to Available section
- Search for "Deploy to Container" plugin
- Click on Install without restart
- Go to the dashboard of Jenkins
- Go to the Development job--->Click on configure
- Go to Post Build actions
- Click on Add Post build action
- Click on Deploy war/ear to container
```
war/ear file: **/*.war
context path: testapp
click on Add container---->Select tomcat9
enter tomcat9 credentials
```
Tomcat url: private_ip_of_QAServer:8080
- Apply---->Save 

This job will deploy the artifact into the QAServer and to access the application from the browser using public_ip_of_qaserver:8080/testapp

4. **Continuous Testing**
- Open the dashboard of Jenkins
- Click on New item--->Enter item name as Testing
- Select Free Style Project---->OK
- Go to Source Code Management
- Select Git
- Enter the giturl where testers have uploaded the selenium test scripts 
  ```
   https://github.com/intelliqittrainings/FunctionalTesting.git 
  ```
- Go to Build section
- Click on Add Buil step
- Click on Execute shell 
  ``` 
  java -jar path_Testingjar/testing.jar 
  ```
- Apply--->Save
- Go to the dashboard of JEnkins--->Go to Testing job--->Click on Build icon

This job will download all the Selenium test scripts and execute them on the application deployed into the QAServer.

5. **Linking Development job to Testing job:**
Development job should be linked with the Testing job so that after all the stages in the Development job it will trigger the Testing job.

- Open the dashoboard of Jenkins
- Go to Development job--->Click on configure
- Go to Post Build actions
- Click on Add Post Build actions
- Click on Buil other projects
- Enter project name as "Testing"
- Apply---->Save

6. **Copying artifacts from Development job and Testing job:**
- Open the dashboard of Jenkins
- Click on Manage Jenkins--->Manage Plugins
- Go to Available section
- Search for "Copy Artifact" plugin
- Click on Install without restart
- Go to the dashboard of Jenkins
- Go to the Development job--->Click on configure
- Go to Post Build actions
- Click on Add Post Build actions
- Click on Archive the artifacts  
   ```
    File to archive: **\*.war 
   ``` 
- Apply--->Save
- Go to the dashbord of Jenkins
- Go to the Testing job---->Click on Configure
- Go to Build section
- Click on Add Build step
- Click on Copy artifacts from other projects
- enter project name as Development
- Save

7. **Continuous Delivery:**
- Open the dashboard of JEnkins
- Go to the Testing job
- Click on Configure
- Go to Post Build actions
- Click on Add post build action
- Click on Deploy war/ear to container
  ```
  war/ear files: **/*.war 
  context path: prodapp 
  click on Add container 
  select tomcat9 
  enter username and password of tomcat9 
  tomcat url: private_ip_of_prodserver:8080 
  ```
- Apply--->Save

 
### 7. What are the alternate ways of installing Jenkins?

1. **Using apt or yum repository in Linux**
 - Update the apt reposiotry and install java
  ```
  sudo apt-get update
  sudo apt-get install -y openjdk-8-jdk
  ```
 - Add the jenkins repository key to the apt repository
 ```
  wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
```
 - Add the debain repository address to jenkins.list file
```
  sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```                                     
 - Update the apt repository
  ```
  sudo apt-get update
  ```
 - Install jenkins
  sudo apt-get install -y jenkins

2. **Setup of Jenkins on tomcat**
 - Update the apt repository
 ```
  sudo apt-get update
 ```
 - Install tomcat9 and tomcat9-admin
 ```
  sudo apt-get install -y tomcat9 tomcat9-admin
 ```
   - Download the jenkins.war
  ```
  wget https://get.jenkins.io/war-stable/2.249.1/jenkins.war
  ```
  - Give wirite permisssions to other on tomcat9 folder
  ```
  sudo chmod o+w -R /var/lib/tomcat9
  ```
 - Copy this war into jenkins
  ```
  cp jenkins.war /var/lib/tomcat9/webapps
  ```
 - To access tomcat from browser
  ```
  public_ip:8080
  ```
 - To access jenkins
 ```
  public_ip:8080/jenkins
 ```

3. **Setup of Jenkins in Docker**
```
docker images
docker run -d --name jenkins -p 8080:80 jenkins/jenkins
docker ps
docker images
curl http://localhost:8080
```

### 7. How to Create users in Jenkins?
- Open the dashboard of jenkins
- click on manage jenkins
- click on manage users
- click on create users
- enter user credentials

### 8. How to Create roles and assign them to users?
- Open the dashboard of jenkins
- click on manage jenkins
- click on manage plugins
- click on role based authorization strategy plugin & install it if it's not already installed
- go to dashboard-->manage jenkins
- click on configure global security
- check enable security checkbox
- go to authorization section-->click on role based strategy radio button
-  apply-->save
-  go to dashboard of jenkins
-  click on manage jenkins
-  click on manage and assign roles
- click on mange roles
-  go to global roles and create a role "employee"
-  for this employee in overall give read access and in view section give all access
-  go to project roles-->Give the role as developer and pattern as Dev.* (ie developer role can access only those jobs whose name start with Dev)
- similarly create another role as tester and assign the pattern as "Test.*"
-  give all permissions to developers and testers
-  apply--save
-  click on assign roles
-  go to global roles and add user1 and user2 
-  check user1 and user2 as employees
-  go to item roles
-  add user1 and user2
-  check user1 as developer and user2 as tester
-  apply-->save

If we login into jenkins as user1 we can access only the development related jobs and user2 can access only the testing related jobs.


### 9. What is Master Slave Architecture of Jenkins and How do we setup it?
This is used distribute the work load to additional linux servers called as slaves. This is used when we want to run multiple jobs on jenkins parallelly.

1. **Setup**
 - Create a new AWS ubuntu20 instance

 - Install the same version of java as present in the master
  ```
  sudo apt-get update
  sudo apt-get install -y openjdk-8-jdk
  ```
 - Setup passwordless SSH betwen Master and slave
 ```
  // Connect to slave and set password to default user
     sudo passwd ubuntu
  // Edit the ssh config file
     sudo vim /etc/ssh/sshd_config
     Search for "PasswordAuthentication" and change it from no to yes
  // Restart ssh
     sudo service ssh restart
  // Connect to Master using git bash & Generate the ssh keys
     ssh-keygen
  // Copy the ssh keys & copy the content of the public keys to a file called "authorised_keys" on the slave machine
     ssh-copy-id ubuntu@private_ip_of_slave
 
 ```
2. **Connect to slave using git bash**
 - Downlaod the slave.jar file
 ```
  wget http://private_ip_of_jenkinsserver:8080/jnlpJars/slave.jar
 ```
 - Give execute permissions to the slave.jar
  chmod u+x slave.jar
 - Create an empty folder that will be the workspace of jenkins mkdir workspace
3. Open the dashboard of Jenkins
4. Click on Manage Jenkins--->Click on Manage Nodes and Clouds
5. Click on New node---->Enter some node name as Slave1
6. Select Permanant Agent--->OK
7. Enter remote root directory as /home/ubuntu/workspace
8. Labels: myslave (This label is associated with a job in jenkins and then that job will run on that slave)
9. Go to Launch Method and select "Launch agent via execution of command on master"
10. Click on Save
11. Go to the dashboard of Jenkins
12. Go to the job that we want to run on slave---->Click on Configure
13. Go to General section
14. Check restrict where this project can be run
15. Enter slave label as myslave

### 10. What is Pipeline as Code?
Implementing all the stages of CI-CD from the level of a Grrovy script file is called as Pipleine as Code. This groovy script files is called as Jenkinsfile and generally it is uploaded into the remote git server along with the application code. From the remote git server this Jenkinsfile will trigger all the stages of CI-CD.
- Below is the Java based project CI/CD declarative pipeline groovy script.

```
pipeline {
    agent {
        label 'master'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
                junit 'target/surefire-reports/*.xml'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying to staging environment...'
                sh './deploy.sh staging'
            }
        }
        stage('Release') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying to production environment...'
                sh './deploy.sh production'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
            mail to: 'devops@example.com',
            subject: "Pipeline failed",
            body: "The pipeline failed. Check the logs for more information."
        }
    }
}
```
This pipeline has four stages: Build, Test, Deploy and Release. The agent block specifies that the pipeline should run on the "master" agent.
1. The Build stage runs the command mvn clean install to build the code.
2. The Test stage runs the command mvn test to run the tests and parse the junit xml test result by junit 'target/surefire-reports/*.xml'
3. The Deploy stage runs a shell script deploy.sh that deploys the code to the staging environment.
4. The Release stage runs the same script deploy.sh but with a different argument production to deploy the code to the production environment, it will only run if the branch is master.
5. The post block specifies actions to take after the pipeline completes, such as sending an email notification if the pipeline fails.

- Below is the C# based project CI/CD declarative pipeline groovy script.
```
pipeline {
    agent {
        label 'Windows'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                bat 'dotnet build'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                bat 'dotnet test --logger:"trx;LogFileName=testResults.trx"'
                publishTestResults (testResults: '**/testResults.trx')
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying to staging environment...'
                bat 'dotnet publish --configuration Release --output deploy'
                bat 'xcopy deploy \\\\stagingServer\\webapp /s /e'
            }
        }
        stage('Release') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying to production environment...'
                bat 'xcopy deploy \\\\productionServer\\webapp /s /e'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
            mail to: 'devops@example.com',
            subject: "Pipeline failed",
            body: "The pipeline failed. Check the logs for more information."
        }
    }
}
```
This pipeline has the same stages as the previous example (Build, Test, Deploy, and Release), but the commands used are specific to a .NET environment.
1. The agent block specifies that the pipeline should run on a Windows slave.
2. The Build stage runs the command dotnet build to build the code.
3. The Test stage runs the command dotnet test to run the tests and parse the test result by testResults.trx using publishTestResults (testResults: '**/testResults.trx')
4. The Deploy stage runs dotnet publish command to create deployable package, and then uses xcopy command to copy the files to the staging server.
5. The Release stage uses the same xcopy command to copy the files to the production server. It will only run if the branch is master.
6. The post block specifies actions to take after the pipeline completes, such as sending an email notification if the pipeline fails.

### 11. What are the advantages of Pipeline as Code?
1. Since the stages of CI-CD are implemented from the level of code it can perform version controlling on it ie it gives the team members ability to edit and review the code along with support for pipeline versioning in various commits and branches. 
2. Jenkinsfile can withstand planned and unplanned restarts of the Jenkins master.
3. It can perform all stages of CI-CD with minumum number of plugins as a result of which it give better perfromance than the free style projects.
4. It can handle all the real time challanges like if conditions, errror handling etc.

### 11. What are the different ways Pipeline as Code can be implemented in Jenkins?
- Pipeline can be implemented in 2 ways
 1. Scripted Pipeline
 2. Declarative Pipeline

- **Scripted Pipeline**
```
node('master')
{
   stage('Stage name in CI-CD')
   {
       Groovy script code for implementing this stage
   }
}
```
- **Declarative Pipeline**
```
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
```
### 12. Can you give me a scripted pipeline example for Java based project?
```
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
  ```  
### 12. Can you give me a scripted pipeline example for Dotnet based project?    
   ``` 
node('windows') 
{
    stage('ContinuousDownload_Master') 
    {
         git branch: 'master', url: 'https://github.com/username/aspnet-project.git'
    }
     stage('ContinuousBuild_Master') 
    {
        bat '"C:\\Windows\\Microsoft.NET\\Framework\\v4.0.30319\\msbuild.exe" /p:Configuration=Release /p:DeployOnBuild=true /p:DeployDefaultTarget=WebPublish /p:WebPublishMethod=FileSystem /p:DeleteExistingFiles=True /p:publishUrl="C:\\inetpub\\wwwroot\\aspnet-project"'
    }
    stage('ContinuousDeployment_Master')
    {
        sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.55.129:/var/lib/tomcat8/webapps/qaapp.war'
    }
    stage('ContinuousTesting_Master')
    {
        bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\Community\\Common7\\IDE\\Extensions\\TestPlatform\\vstest.console.exe" /logger:trx /TestAdapterPath:"C:\\inetpub\\wwwroot\\aspnet-project\\test\\bin\\Debug" "C:\\inetpub\\wwwroot\\aspnet-project\\test\\bin\\Debug\\aspnet-project.test.dll"'
                publishTestResults (testResults: '**/*.trx')
    }
     stage('ContinuousDelivery_Master')
    {
       
        bat 'net stop w3svc'
                bat 'xcopy "C:\\inetpub\\wwwroot\\aspnet-project\\bin\\Release\\Publish" "C:\\inetpub\\wwwroot\\aspnet-project" /s /e'
                bat 'net start w3svc'
    }

}
  ``` 
 
### 13. How to create pipeline as code project in Jenkins?
1. Open the dashboard of Jenkins
2. Click on New item--->Enter some itemname
3. Select Pipeline project--->OK
4. Go to Pileline section--->Select Pipeline script from SCM
5. Select SCM as Git
6. In Repository url: Enter the github url where we uploaded the code
7. Click on Apply--->Save

### 14. How to create declarative pipeline with post conditions?
Declarative Pipeline with Post Conditions
 ``` 
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
   ``` 
  
### 15. What are CatLight notifications and How do we setup to get notifications? 
This is a client side s/w which is used to send notifications of jenkins jobs in the form of simple pop msgs. CatLight has to be installed on every individual team members machines/
1. Open https://catlight.io/downloads
2. Download and install catlight for windows
3. Open cat light and it will display the list of CI tools that it can connect to
4. Select JEnkins
5. Enter the public_ip_of_jenkins_Server:8080
6.  Enter username and password of jenkins
7. Catlight will display the list of jobs available in jenkins
8. Select the jobs for which we need notifications
9. Run that job in Jenkins and we will get a desktop notification

### 14. How to create declarative pipeline with exception handling?
``` 
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
``` 

### 15. How to create scripted pipeline with exception handling?
```
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
```

### 16. What are Wehooks? How do we setup them in Jenkins? 
Webhooks used to send notifications from git server to jenkins whenever any code changes are done and that is checkdin into git. Webhook will send an immediate notifiction to Jenkins and Jenkins will trigger the job that has subscribed to webhook.

1. Open github.com---->Click on the reposiotry that we are working on
2. On the right corner clikc on Setting
3. Click on Webhooks in the left pannel
4. Click on Add Webhook
5. In Payload URL: http://public_ip_jenkinsserver:8080/github-webhook/
6. In Content type select :application/json
7. Click on Add Webhook
8. Open the dashboaard of Jenkins
9. Go to the job that we want to configure
10. Go to Build triggers
11. Check GitHub hook trigger for GITScm polling
12. Click on Apply--->Save

Now if we make any changes to the code in github then github will send an notification to jenkins and jenkins will run that job.


### 16. What is MultiBranch Pipeline?
Developers upload multiple functionalities code on different branches. On each of these branches there will be a copy of the Jenkinsfile which has CI with or without CD instructions of what should be done on that branch.

- **Setting up mulitbranch pipeline project in Jenkins**
1. Open the dashboard of Jenkins
2. Click on New item---->Enter item name as MultBranchPipeline
3. Select MultiBranchPipeline--->OK
4. Go to Branch Sounrces---->Select Git-->enter github url where developers uploaded the code
5. Go to Scan Multi branch pipeline triggers---->Select 1 minute
6. Apply--->Save

### 16. Give an example for MultiBranch declarative Pipeline as Code for Java?
```
pipeline {
    agent {
        docker {
            image 'node:lts-alpine'
            args '-p 3000:3000 -p 5000:5000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development' 
            }
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'  
            }
            steps {
                sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
```

### 17. Give an example for using docker containers as agents?
 1. Create a specific node as agent.
```
pipeline {
  agent {
    docker { image 'node:16-alpine' }
  }
  stages {
    stage('Test') {
      steps {
        sh 'node --version'
      }
    }
  }
}
```
2. Create an agent specific to stage
```
pipeline {
  agent none
  stages {
    stage('Back-end') {
      agent {
        docker { image 'maven:3.8.1-adoptopenjdk-11' }
      }
      steps {
        sh 'mvn --version'
      }
    }
    stage('Front-end') {
      agent {
        docker { image 'node:16-alpine' }
      }
      steps {
        sh 'node --version'
      }
    }
  }
}
```
3. With dockerfile in the repository
 - **jenkinsfile**
```
pipeline {
  agent { dockerfile true }
  stages {
    stage('Test') {
      steps {
        sh '''
          node --version
          git --version
          curl --version
        '''
      }
    }
  }
}
```
 - **dockerfile**
 ```
FROM node:16-alpine
RUN apk add -U git curl
```
### 17. Why would you want to use an image that turns into a container as your build agent? 
1. As a pipeline author it gives us the capability to define the tools and specific versions of those tools that we want to use in our pipeline. So that those items are not being mandated by others. 
2. If in our environment someone else has to install the tools for our agent, we can completely bypass all of that because we're able to dynamically bring in the tools that we want at runtime.
3. It gives us the chance to experiment with different tools without having to make a long-term commitment to those tools because if in the case of VM agent we have a dependency on someone else installing tools for us which might take a long time. But by running it as container we have the freedom to test the tools we want later which we can use static versions of those tools in production environmet agent if needed or we just stay with your container-based build agents.









































 





 




























































 













































































