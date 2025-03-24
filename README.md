
Jenkins by KK FUNDA
====================

Explain the flow diagram : developer --> GitHub --> maven --> SonarQube --> Nexus --> Tomcat  --> mail


Jenkins
=======

IQ] what is Jenkins?

-->Jenkins is an open source Continuous Integration tool, cross-platform tool, written in Java.

--> Kohsuke Kawaguchi is Creator of the Jenkins CI server in 2004

-->Initially, it was called Hudson, but in 2011 it was renamed to Jenkins

Advantages  of Jenkins
======================
--> It’s an open source tool with great community support.

--> Easy to install and It has a simple configuration through a web-based GUI, which speeds up the Job[deployment process]

--> It has around 1900+ plugins to ease your work. If a plugin does not exist, just code it up and share with the community (https://plugins.jenkins.io/).

--> Its built with Java and hence, it is portable on all major platforms.

--> Good documentation and enriched support articles/information available on internet which
will help beginners to start easy.


Continuous Integration[CI]:
==========================

---> explain diagram 

Continuous Integration (CI) is the process of automating the build and testing of code every time a team member commits changes to version control.

(OR)

Continuous Integration is a development practice where developers integrate their code into a shared remote repository frequently, preferably several times a day. Each integration is verified by an automated build (including test) to detect integration errors as quickly as possible.


CI Advantages
-------------
--> Immediate bug detection
--> Less Merge Conflicts
--> Deploy an application at any given point
--> Improved Code Quality [Consistent Testing, Code Reviews]
--> Developers receive immediate feedback on their code changes, allowing them to address issues     promptly.



Continuous Delivery:
====================
every successful build that has passed all the relevant automated tests and quality gates can potentially be deployed in to production via fully automated one click process.

diagram 
-------

code done --> unit tests --> Integrate --> Acceptance Test ---> Deploy into production
         AUTO           AUTO          AUTO                 MANUAL 

NOTE: Once we get the approval from the client and the sign-off mail from the QA team then we are going   to deploy
 

Continuous Deployment: 
======================

The practicing of automatically deploying every successful build directly into production without any manual steps knows as Continuous deployment.


code done --> unit tests --> Integrate --> Acceptance Test ---> Deploy into production
         AUTO           AUTO          AUTO                 AUTO 



IQ] Which one you are using continuous delivery or continuous deployment ?

ANS: I involved in many projects so we are using continuous deployment in "IN-HOUSE PROJECTS"   
     
      EX: Company internal Project : HR ---> 

    Coming to continuous delivery , We used for "client (external) projects"

     EX: jio, flipkart, amazon, etc




What Jenkins can do?


• Integrate with many different Version Control Systems (GitHub, BitBucket , GitLab, ...)
• Generate test reports (JUnit)
• Push the builds to various artifact repositories[nexus/jfrog]
• Deploys directly to production or test environments
• Notify stakeholders of build status (Through Email/slack,etc)



List of popular Continuous Integration tools
============================================

SNO     Product           Is Open Source?
===========================================
1       Jenkins              Yes  [community edition]
2       Cloudbees Jenkins    No   [Enterprise edition] 
2       Bamboo               No
3       Cruise Control       Yes
4       Travis CI            Yes and Paid also
5       Circle CI            Yes and Paid also
6       GitLab CI            Yes and Paid
7       TeamCity             Yes and Paid



NOTE: default port for jenkins: 8080

8080 --> tomcat

8081 --> nexus

9000 --> SQ

Jenkins Installation
====================
prerequsite : JAVA, min: t2.medium

JAVA Installation
-----------------

step 1: launch an ec2 machine(t2.medium), connect to that machine

step 2: switch to root user [sudo su - ]

step 3: javac --version

java 11
-------
sudo yum install java-11-openjdk-devel -y

sudo yum install java-17-openjdk-devel -y

yum install fontconfig java-17-openjdk



java -version


JENKINS Installation
====================

--> LTS[Long Term Support] ---> stable version without any issues.
--> search on google [ download jenkins ] --> LTS --> Redhat/fedora/centos


step 1: sudo su -

step 2: 

yum install wget -y


sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
  

step 3: 
   yum install jenkins -y

step 4: 
 systemctl enable jenkins

step 5: 

  systemctl status jenkins
  systemctl start jenkins
  systemctl status jenkins

step 6: 

http://13.201.93.75:8080/  --> please make sure to enable 8080 port 

cat /var/lib/jenkins/secrets/initialAdminPassword

step 7:

click on suggested plugins

step 8:

user_name:  kkfunda
password: kkfunda
confirm password: kkfunda
Full Name: KK FUNDA

save And Continue  --> Save and finish --> start using jenkins 



========================================================================================



















SonarQube installation
======================

step 1: launch t2.medium machine [4GB]

step 2: connect to that server

step 3: switch to root user [ sudo su - ]

step 4: install java

   sudo yum install java-11-openjdk-devel -y
  
   javac --version

step 5: go to /opt dir

  cd /opt

step 6: yum install wget unzip -y

step 7: wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.6.1.59531.zip

step 7.1 : unzip sonarqube-9.6.1.59531

step 8: mv sonarqube-9.6.1.59531 sonarqube

step 9: 
 As a good security practice, SonarQuber Server is not advised to run sonar service as a root user, so create a new user called sonar user  and grant sudo access to manage nexus services as follows.


useradd sonar

step 10: 

Give the sudo access to sonar user

visudo

sonar   ALL=(ALL)       NOPASSWD: ALL

step 11:

Change the owner and group permissions to /opt/sonarqube/ directory.


chown -R sonar:sonar /opt/sonarqube/
chmod -R 775 /opt/sonarqube/
su - sonar
cd /opt/sonarqube/bin/linux-x86-64/

sh sonar.sh start
sh sonar.sh status

in real time same permission are given to the file ?



step 12: Now you can try to access the SonarQube Server.

NOTE: default port number for Sonarqube server: 9000

http://15.207.110.48:9000

NOTE: pls make sure to allow traffic for 9000 port.

step 13: refresh the page

  default credentials:  uname: admin   pwd: kkfunda

step 14: It will ask to change the password



========================================================================================

Nexus Installation starts
========================



step 1: Launch an EC2 instance [t2.medium]

step 2: connect to that server.

step 3: Before installation check the RAM once: " free -h "

step 4: sudo su -

step 5: check whether java is installed or not.

     javac -version

step 6: Install java
 
#Install JDK 1.8 
sudo yum install java-1.8.0-openjdk-devel -y

javac -version

step 7: 

cd /opt	

yum install tar wget -y

step 8: 



https://download.sonatype.com/nexus/3/nexus-3.70.1-02-java8-unix.tar.gz

wget https://download.sonatype.com/nexus/3/nexus-3.70.1-02-java8-unix.tar.gz


step 9: 

tar -zxvf nexus-3.70.1-02-java8-unix.tar.gz


step 10:

mv /opt/nexus-3.70.1-02 /opt/nexus



NOTE: As a good security practice, Nexus is not advised to run nexus service as a root user, so create a new user called nexus and grant sudo access to manage nexus services as follows.


step 11: 

useradd nexus

step 12: Give the sudo access to nexus user

visudo
nexus ALL=(ALL) NOPASSWD: ALL

step 13: Change the owner and group permissions to /opt/nexus and /opt/sonatype-work directories.

chown -R nexus:nexus /opt/nexus
chown -R nexus:nexus /opt/sonatype-work
chmod -R 775 /opt/nexus
chmod -R 775 /opt/sonatype-work


step 14: Open /opt/nexus/bin/nexus.rc file and  uncomment run_as_user parameter and set as nexus user.

vi /opt/nexus/bin/nexus.rc
run_as_user="nexus"

step 15: Create nexus as a service

ln -s /opt/nexus/bin/nexus /etc/init.d/nexus


step 16: Switch as a nexus user and start the nexus service as follows.

sudo su - nexus

step 17: Enable the nexus services

sudo systemctl enable nexus

step 18: Start the nexus service

sudo systemctl start nexus

step 19:  Access the Nexus server from Laptop/Desktop browser.

http://65.1.95.162:8081/

step 20: click on login

NOTE: Before 3.15 version uname and password is admin and admin123 , But now process changed.

cat /opt/sonatype-work/nexus3/admin.password

Uname: admin   pwd: kkfunda

===============================================================================================


Installation of tomcat
======================

prerequisites 
-------------
java 1.8 min required for tomcat 9.x version.

1 GB RAM is enough, because  we are running small web application.

step 1: launch one ec2 m/c for tomcat 

step 2: connect to that server

step 3: sudo su -

step 4: install java
   sudo yum install java-11-openjdk-devel -y
   javac --version

step 5: yum install wget unzip -y

step 6: cd /opt/
   
      wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.91/bin/apache-tomcat-9.0.91.zip
     
step 7: unzip apache-tomcat-9.0.91.zip

 



step 8: goto the bin directory.
     
       cd /opt/apache-tomcat-9.0.91/bin

step 9: chmod u+x *.sh


IQ] How to start/stop the tomcat server?

    step 1: go to bin directory 

    step 2: sh startup.sh    ----> to start
                or
            sh catalina.sh start ---> to start

          sh shutdown.sh  ----> to stop 
               or
          sh catalina.sh stop ----> to stop


NOTE: By default port number of tomcat : 8080




IQ] How to check tomcat is running or not?

    sudo yum install lsof
    lsof -i :8080


   ps -ef|grep -i "tomcat"







IQ] I want to start/stop tomcat server from anywhere instead of bin dir?


ln -s /opt/apache-tomcat-9.0.91/bin/startup.sh /usr/bin/startTomcat
ln -s /opt/apache-tomcat-9.0.91/bin/shutdown.sh /usr/bin/stopTomcat

Now you can go and run in any directory.


http://13.201.60.70:8080/












IQ] How to access tomcat server from PC?

NOTE: default port number for tomcat server is 8080.

 http://65.2.129.199:8080  ---> directly you cant access without enable that port number     				in security group.

  select the server --> go to security --> scroll down --> click on security group ---->
  click on edit in-bound rules ---> click on add rule ---> select custom tcp ---> give port 8080 ----> select anywhere ipv4 ---> save the rules.

Then reload this url http://13.233.32.177:8080

click on server Status, Manager App, Host Manager ----> not able to access.


====================================================================


--> we can place our application into "Manager App"
                                       ===========

step 1: cd /opt/apache-tomcat-9.0.91/webapps

step 2: cd manager 

step 3: cd META-INF

step 4: ls ----> context.xml

step 5: vi context.xml
    
      :se nu
      comment 21st and 22nd lines.
     <!--
     -->
step 6: refresh the main page ----> It will ask the credentials.

step 7: cd /opt/apache-tomcat-9.0.91/conf/ 

step 8: vi tomcat-users.xml ---> goto end of the file and add users.

  <user username="kk" password="kkfunda123" roles="manager-gui,admin-gui"/>

  <user username="mahesh" password="mahesh" roles="manager-gui,admin-gui"/>



if you want to login Host-manager do the same process?
                     ============
step 1: cd /opt/apache-tomcat-9.0.91/webapps

step 2: cd host-manager 

step 3: cd META-INF

step 4: ls ----> context.xml

step 6: vi context.xml

step 7: vi context.xml

      comment 21st and 22nd lines.
     <!--
     -->
step 8: refresh the main page ----> It will ask the credentials, give the credentials.

step 9: go and check the logs directory logs are created or not

       cd /opt/apache-tomcat-9.0.91/logs

  uname: admin	pwd: kkfunda


=================================================================================================

Automate all the tasks using jenkins
=====================================

How to create a job
===================

Jenkins DashBoard --> New item --> enter an item name(jio-dev) --> freestyle project --> ok --> general --> description --> scroll down --> source code management -->  select git(GitHub,bitbucket,gitlab) --> repository url --> After that we will get an error --> pls install git in jenkins server --> yum install git -y --> save --> click on configure for any updates --> 


How to add git credentials
--------------------------

click on add --> uname: kkeducation12345 pwd: ghp_C9W7WSKt9dryxCkzU7mqQc1X6lUJOX47cPL7  --> Description --> github credentials --> Add 

--> branches to build --> */development --> scroll down --> build -->add build --> Invoke maven toplevel targets ---> goals --> save 


--> for run the job click on job --> In left side click on buid now --> failed --> click on job --> console output --> Due maven not instaled uild is failing 

--> check maven is installed or not in jenkins server 

  mvn -version


IQ] Where we need to install maven in linux server or in the jenkins server itself ?

ANS: If you go for linux server only one maven install is possible but in jenkins many versions possible so we are going to install in the jenkins server.



How to download maven in jenkins ?
==================================

go to jenkins dashboard --> manage jenkins --> tools -->scroll down --> add maven -->  maven 3.9.8 --> select version 3.9.8 --> add many versions --> save 

click on job --> configure --> scroll down --> build steps -->  select maven version --> save 

--> again run the job --> It will success 


/var/lib/jenkins/workspace/jio-dev/target/ --> warfile location




SonarQube server integration
============================

take ip address of SonarQube server [http://15.207.110.48:9000/] --> go to GitHub repository --> select the correct branch [development] --> pom.xml --> edit the file --> in <properties> tag keep sonarqube server details 


--> go to job --> configure --> scroll down --> build [ clean package sonar:sonar ] --> save

--> go and see the sonarqube server --> check the projects --> now build the job --> success.





Nexus integration with jenkins
===============================

step 1: connect to maven server, Where java projects are available

step 2: where to keep our repository details?

update the details in pom.xml

          <distributionManagement>

            <repository>
              <id>nexus</id>
              <name>KK FUNDA Releases Nexus Repository</name>
              <url>http://65.1.95.162:8081/repository/jio-release/</url>
            </repository>

            <snapshotRepository>
              <id>nexus</id>
              <name>KK FUNDA Snapshot Nexus Repository </name>
              <url>http://65.1.95.162:8081/repository/jio-snapshot/</url>
            </snapshotRepository>

        </distributionManagement>

step 3: Where we need to keep nexus credentials?

--> In SonarQube we updated credentials in pom.xml


NOTE: maven is installed in jenkins pls check correct path of settings.xml


find / -name settings.xml

--> In nexus, repo details in pom.xml and credentials in 
 cd /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven_3.9.8/conf/


   <server>
      <id>nexus</id>
      <username>admin</username>
      <password>kkfunda</password>
    </server>


--> click on job --> configure --> build --> clean deploy sonar:sonar --> save build now 


tomcat integration
==================







==============================================================================================






















discard old builds
===================

create an another job with same configuration of other job
========================================================== 



To automate build ?

1. pool SCM    ----> waiting for updated code 
============
* * * * *

jenkins ---> github[development] --> commit ids 


deveploper --->




2. build periadically --> Not waiting for updated code . follows time
=====================
* * * * * 

jenkins ---> github --> devlopment -->


3. github webhook
==================

github --> jenkins ---> At the time of updated code.


code coverage not reached to 80%  
--------------------------------

Jacoco
======



jenkins directory structure
===========================


default path: /var/lib/jenkins/


jobs
====

all job informartion

   builds 

     12
     13
     14 

logs 
----

workspace
----------

tools
======

users
=====

nodes 
====


plugins
==========



==============================================================================================

Jenkins server stop and start issue
====================================

old: 52.66.196.163

new: 65.2.171.155


now ip we r changing in jen.model.jenconf.xml it affects in all other tools also??


Disable and eanble the build
=============================


1:00 AM to 3 AM --> tomcat sever down --> 15days


























Plugins in jenkins server
=========================

Deploy to container*
===================

--> Deploy the our application into the tomcat server 








maven integration
==================

if you want to create a maven project type then use this plugin.

















safeRestart
===========

systemctl restart jenkins ---> It is in linux server, But we dont have permission to access it , Then how to restart it.


restart --->http://65.0.199.60:8080/restart

safeRestart -->http://65.0.199.60:8080/safeRestart

IQ] what is the difference between restart and safeRestart ?

restart: It will stop the running jobs and then restarted

safeRestart: It will wait for complition of all the jobs and restarted


NOTE: for safeRestart we have plugin called as a safeRestart, Install and try it














next Build Number
=================

--> After insatlling this plugin we can give our own build number, The next number must be greater than the previous build number only.

NOTE: in linux server /var/lib/jenkins/jobs/jio-dev/jobs/nextBuildNumber file is available , But some time times we dont have an access to linux server to use this

















JaCoCo
======

By using this plugin we can stop the deployment through code coverage percentage.










ssh agent 
=========
we will discuss in the pipeline project

Audit Trail ***
===========

create, delete , update ----> log files

audit-trail.log.0

audit-trail.log.1

audit-trail.log.2

audit-trail.log.3











Job Configuration history
=========================

It will store the deleted jobs




















Blue ocean plugin
=================

















Build name Description setter
=================


Thin backup 
===========
will discuss in jenkins backup

Role based authentication
=========================
will discuss in jenkins security


=====================================================================================

Build with parameters
======================



How to create a view?
=====================

jenkins security
================










===========================================================================



How to integrate with slack?
=============================

step 1: login slack.com

step 2: channels --> chanel --> create channel --> channel name --> next --> public --> create

step 3: 

    KK FUNDA --> Invite pople to kk funda --> copy invite link 

   https://join.slack.com/t/kkfunda/shared_invite/zt-2nxl4nw11-LipxXXbLvOotWPmIIPjFgw


step 4: KK FUNDA --> tools and settings --> manage apps --> search with "jenkins ci" --> click on "Add to slack" --> select a channel --> Add jenkins ci integration --> 

https://kkfunda.slack.com/services/B07F7MKPJ13?added=1

step 5: install slack notification plugin in jenkins

step 6: manage jenkins --> configure systems --> slack --> workspace: kkfunda -->

   credentials: Add credentials --> Secret text --> paste the secret[lHCwhkIRdaeAqZlRaYEqi2mQ] --> add the description

    default channel: #jio ---> Test connection --> save

step 7: 

select job --> configure --> scroll down to end --> post build actions --> select slack notifications 

--> select slack notifications --> advanced --> select options --> save 


==================================================================================================

Jenkins security
================

--> procedure of providing security to the jenkins server called as jenkins security.

IQ] where the jenkins users information will store?

Ans: /var/lib/jenkins/users/users.xml


For example
===========

kkfunda --> devops engineer
prasanth --> devops engineer

jaswanth --> developer
raghu    --> developer

IQ] How to create a user in jenkins?

manage jenkins --> manage users --> create users --> 

  uname :prasanth
  pwd   :kkfunda
  conform pwd: kkfunda
  full name: prasanth
  email: abc@gmail.com

NOTE: by default every user has admin access , How to give read access to developers?

--> [Install role based authorization startegy  plugin]

--> login as a admin	--> manage jenkins --> security --> security --> authentication --> Authorization 

--> select Project based matrix Authorization Strategy

NOTE: add all users and give the permissions, check the activities.


====================================================================================================















Freestyle job
Maven job

NOTE: we can not customize the job using maven and free style[ EX: order of exexution]

Create the pipeline project job
===============================

--> Pipeline scripts can be written in the groovy script.

--> we can write in two ways
   1. scripted way
   2. declarative way


NOTE: pls install stageview plug-in

1. scripted way
===============

syntax:
=======

node //by default  built-in(master) node
{

//write code here.

}

step 1: create a pipeline job

goto new item --> Enter an item name(demo-scripted-pipeline) --> pipeline --> ok

step 2: get the code from github repository

select pipeline-job--> configure --> scrool down to pipeline area --> click on pipeline syntax --> sample step --> git: Git

   Repo url: 
   branch:
   credentials:
   
--> generate pipeline script



node
{
   stage('checkout')
   {
   git branch: 'development', credentialsId: 'e5b73679-3105-4429-a5b4-b303fd9e35a0', url: 'https://github.com/kkeducation12345/maven-web-app-project-kk-funda.git'
   }
}


step 3: 

node
{
   def mavenHome=tool name: "maven 3.9.8"
   stage('checkout')
   {
   git branch: 'development', credentialsId: 'e5b73679-3105-4429-a5b4-b303fd9e35a0', url: 'https://github.com/kkeducation12345/maven-web-app-project-kk-funda.git'
   }
   stage('build')
   {
  sh "${mavenHome}/bin/mvn clean package"
   }
  
}


step 4: execute the sonarqube report

node
{
   def mavenHome=tool name: "maven 3.9.8"
   stage('checkout')
   {
   git branch: 'development', credentialsId: 'e5b73679-3105-4429-a5b4-b303fd9e35a0', url: 'https://github.com/kkeducation12345/maven-web-app-project-kk-funda.git'
   }
   stage('build')
   {
  sh "${mavenHome}/bin/mvn clean package"
   }
  stage('SonarQubeReport')
   {
  sh "${mavenHome}/bin/mvn clean package sonar:sonar"
   }
  
}


step 5:  upload artifact into nexus

node
{
   def mavenHome=tool name: "maven 3.9.8"
   stage('checkout')
   {
   git branch: 'development', credentialsId: 'e5b73679-3105-4429-a5b4-b303fd9e35a0', url: 'https://github.com/kkeducation12345/maven-web-app-project-kk-funda.git'
   }
   stage('build')
   {
  sh "${mavenHome}/bin/mvn clean package"
   }
  stage('SonarQubeReport')
   {
  sh "${mavenHome}/bin/mvn clean package sonar:sonar"
   }

 stage('Uploadarifacttonexus')
   {
  sh "${mavenHome}/bin/mvn clean package sonar:sonar deploy"
   }
  
}



step 6: deploy application into tomcat server

--> Deploy the application through admin console
--> copy paste the war file into the webapps directory

--> But Jenkins is in different server and tomcat is in different server.

NOTE: now you need to copy file from jenkins server to tomcat server with the help of SCP command , But we need tomcat credentials to pass.

--> Jenkins unable to enter the credentials, So we need to generate the one "SSH token"

--> insatall the "ssh agent" plugin 

--> select the pipeline job --> pipeline syntax --> snippet generator --> [refresh that page] --> sample step  --> sshagent :SSH Agent

--> copy the penfile of tomcat server --> add --> jenkins --> username with private key --> 

description: tomcat credentials
user-name: ec2-user
private key --> enter directly --> add --> paste pem --> add --> generate pipeline script --> add in the stage.


node
{
   def mavenHome=tool name: "maven 3.9.8"
   stage('checkout')
   {
   git branch: 'development', credentialsId: 'e5b73679-3105-4429-a5b4-b303fd9e35a0', url: 'https://github.com/kkeducation12345/maven-web-app-project-kk-funda.git'
   }
   stage('build')
   {
  sh "${mavenHome}/bin/mvn clean package"
   }
  stage('SonarQubeReport')
   {
  sh "${mavenHome}/bin/mvn clean package sonar:sonar"
   }

 stage('Uploadarifacttonexus')
   {
  sh "${mavenHome}/bin/mvn clean package sonar:sonar deploy"
   }

   stage('deployapptotomcat')
   {
     sshagent(['ff0ba357-7dea-4d4c-bf8f-daffd5c1b173']) 
    {
    
     sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.201.194.103/:/opt/apache-tomcat-9.0.91/webapps/"


     }

     sshagent(['29ffdf5c-84b7-4a5a-aade-e5ca6dd35b6f']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.201.194.103:/opt/apache-tomcat-9.0.91/webapps/"
}
   }
  
}


--> After building you will get an error; permission denied [for ec2-user no permission on webapps directory] , Now give the full permissions to webapps directory.

chmod -R 777 webapps

--> again build it will be sucess.



================================================================================================


How to configure poll SCM?
==========================

jenkins --> select pipeline job --> pipeline syntax --> snippet generator --> properties: Set job properties --> select discard old builds

           --> poll scm
               * * * * *
---> generate script --> copy --> paste at node level



//This is scripted pipeline sample
node
{

  properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '5', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * * ')])])
  //   /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven-3.9.9/bin

   def mavenHome=tool name:  "maven-3.9.9"
  stage('git checkout')
  {
  git branch: 'development', credentialsId: 'd8f5bb40-ee7a-41f2-a72d-0fcc8eb6b07b', url: 'https://github.com/kkeducation12345/maven-web-app-project-kk-funda.git'
  }
  stage('Build')
  {
     sh "${mavenHome}/bin/mvn clean package"
  }
  stage('SQ Report')
  {  
     sh "${mavenHome}/bin/mvn clean sonar:sonar"   
  }

  stage('upload artifactt')
  {
    sh "${mavenHome}/bin/mvn clean deploy"
  }

 /* stage('DeployIntoTomcat')
  {
   sshagent(['12448eed-30eb-4f85-836d-1aae3fa0bee2']) 
   {

    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.201.194.103:/opt/apache-tomcat-9.0.97/webapps/"
    
   }
  } */

stage("Tomcat Deployment")
{
    sshagent(['29ffdf5c-84b7-4a5a-aade-e5ca6dd35b6f']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.201.194.103:/opt/apache-tomcat-9.0.97/webapps/"
}
}    
}









=====================================================================================


Global variable reference
==========================

jenkins --> select pipeline job --> pipeline syntax--> global variable reference --> click here

node
{
   echo "git branch name: ${env.JOB_NAME}"
   echo "build number is: ${env.BUILD_NUMBER}"
   echo "node name is: ${env.NODE_NAME}"
}



NOTE: In real time jenkins script is placed in the github 


--> copy file --> add file in git hub[Jenkinsfile] --> paste --> goto jenkins job --> pipeline Definition --> select pipeline Script from SCM.


IQ] Is it possible to give the custom name of jenkins file?

ANS: yes

--> edit file name in github --> and trigger the build --> error: unable to find the jenkins file


-->select job --> configure --> change the script path with latest name --> save.


--> Then trigger the build.






How to send slack notications through pipeline?
===============================================


node {
    try {
        notifyBuild('STARTED')

        stage('Prepare code') {
            echo 'do checkout stuff'
        }

        stage('Testing') {
            echo 'Testing'
            echo 'Testing - publish coverage results'
        }

        stage('Staging') {
            echo 'Deploy Stage'
        }

        stage('Deploy') {
            echo 'Deploy - Backend'
            echo 'Deploy - Frontend'
        }

  } catch (e) {
    // If there was an exception thrown, the build failed
    currentBuild.result = "FAILED"
    throw e
  } finally {
    // Success or failure, always send notifications
    notifyBuild(currentBuild.result)
  }
}

def notifyBuild(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary)
}



=========


Freestyle job
maven job


1. scripted way
================



node
{
    echo "Build number is: ${env.BUILD_NUMBER}
    echo " node name is:${env.NODE_NAME}
   
   properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])

   def mavenHome= tool name:"maven 3.9.8"
   //this is first stage 
   stage('git checkout')
   {
    git branch: 'development', credentialsId: 'c13d2b4c-1f45-454d-96b4-0f4dae4cc207', url: 'https://github.com/kkeducation12345/maven-web-app-project-kk-funda.git'
   }
   stage('Build')
   {
      sh "${mavenHome}/bin/mvn clean package"
   }
    stage('SonarQube report')
   {
      sh "${mavenHome}/bin/mvn clean sonar:sonar"
   }

   stage('Deploy artifact')
   {
      sh "${mavenHome}/bin/mvn clean deploy"
   }

    stage('Deploy App to tomcat')
   {
  sshagent(['580bc4fc-5845-4383-9a2a-c7840039f481']) 
      {
   
      sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.200.135:/opt/apache-tomcat-9.0.91/webapps/"
    
      }
     
   }
   
}//node ending 



slack notification in scripted way
===================================


node {
  properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
 def mavenHome= tool name:"maven 3.9.8"
    try {  
   

        
  } catch (e) {
    // If there was an exception thrown, the build failed
    currentBuild.result = "FAILED"
  } finally {
    // Success or failure, always send notifications
    notifyBuild(currentBuild.result)
  }
}//node ending


def notifyBuild(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary)
}




Declarative pipelines
======================


pipeline {
    agent any 
tools
{
  maven "maven 3.9.8"
}

    stages {
        stage('checkout stage') { 
            steps {
              git branch: 'development', credentialsId: 'c13d2b4c-1f45-454d-96b4-0f4dae4cc207', url: 'https://github.com/kkeducation12345/maven-web-app-project-kk-funda.git'
                
            }
        }
            stage('Build') { 
            steps {
         sh "mvn clean package"
                
            }
          }
          stage('SQREPORT'){
            steps{
          sh "mvn sonar:sonar"
          }
        }
         stage('DeployTONexus'){
           steps{
          sh "mvn deploy"
          }
        }
        stage('DeployAppToTomcat'){
           steps{
         sshagent(['580bc4fc-5845-4383-9a2a-c7840039f481']) 
      {
   
      sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.200.135:/opt/apache-tomcat-9.0.91/webapps/"
    
      }

         
          }
        }
    } //stages closing
post {
  success {
    notifyBuild(currentBuild.result)
  }
  failure {
notifyBuild(currentBuild.result)
      }
}
}//pipeline closing


def notifyBuild(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary, channel: '#airtel-dev')
}


===============================================================

Multi Branch Pipleline
======================


Jenkins Backup
==============
Thin backup -----> plugin name



backup   restore   settings


                   --> global configuration


Build with parameters
=======================




pipeline {
    agent any 
tools
{
  maven "maven 3.9.8"
}

    stages {
        stage('checkout stage') { 
            steps {
              git branch: 'development', credentialsId: 'c13d2b4c-1f45-454d-96b4-0f4dae4cc207', url: 'https://github.com/kkeducation12345/maven-web-app-project-kk-funda.git'
                
            }
        }
   stage('Build and SQR')
   {
     steps
     {
        parallel(
      "Build" : {
           sh "mvn clean package"
       },
      "Sonar" : {
           sh "mvn sonar:sonar"
       }
        )
       
     }
   }             
    } //stages closing
}//pipeline closing


Jenkins master slave architecture
==================================

--> MS architechture used to imrove the performance.
--> If you trigger all jobs at a time , generally perfomance will decrease.
--> Another name of node is slave


IQ] Where the jobs information wil stored either slave or master?

Ans: All the jobs information stored in the master


IQ] where the source code will be store?

Ans: Slave machine 

IQ] How many slave machines in your project?
 5 or 6

NOTE: In every slave machine please install java and git


================================================================================

step 1: Create a slave machine

step 2: connet to slave machine, created one folder(node1)

  /home/ec2-user/node1/

step 3:

credentials.sh

uname="kkfunda"
pwd="password"


Display.sh


source credentials.sh
echo "$uname"



===
====
===
===



==============




 















      





























      
