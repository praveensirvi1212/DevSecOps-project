# DevSecOps project using Git, GitHub, Jenkins and SonarQube
An end to end CI-CD projects implementing DevSecOps principles


In this project, we will be see how to *use Git, GitHub , Jenkins,SonarQube and  DEPLOY on a AWS EC2.,*

*Follow this project *

![](https://github.com/praveensirvi1212/jenkins_sonarqube_basic_project/blob/main/images/Screenshot%20from%202023-02-16%2011-50-23.png)

#### PreRequisites
1. Git
1. Github
1. Jenkins
1. SonarQube 
1. AWS EC2
1. Java open-jdk 11
1. Maven


### Stage-01 : Install JDK and Create a Java Springboot application
Put all the web application page code file into github

![](https://github.com/praveensirvi1212/jenkins_sonarqube_basic_project/blob/main/images/Screenshot%20from%202023-02-16%2012-03-55.png) 

### Stage-02 : Install Jenkins and start Jenkins 
1. Install sonarqube scanner plugins
1. go to manage jenkins > manage pulgins > search for plugins > install without restart 

### Stage-03 : Install Postgre Database and Install SonarQube
1. Create a Project Manually
1.  Give name to your project , Project key then click on setup
1.  Click on other ci and generate token
1.  Copy that token and save somewhere because we need this token later.
![](https://github.com/praveensirvi1212/jenkins_sonarqube_basic_project/blob/main/images/Screenshot%20from%202023-02-16%2012-47-08.png) 
  
 ### Stage-04 : Configure Jenkins
1. go to manage jenkins > Manage Credentials > system > Add credentials > secret text file > paste  token we create in sonarqube and save and apply.
1. go to manage Jenkins > Global tool configuration >  Add Maven and SonarQube Scanner
1. go to manage Jenkins > Configure System > Add SonarQube Server 

### Stage-05 : Create a Pipeline Job in Jenkins
1. go to new item > enter item name > Pipeline > ok
1. go to pipeline and create your pipeline script and save and apply
1. Click on Build now to build your job
1. to see output of the build ,  click on build > console output

![](https://github.com/praveensirvi1212/jenkins_sonarqube_basic_project/blob/main/images/Screenshot%20from%202023-02-16%2012-51-35.png) 


### Final output :
Jenkins Output :

![](https://github.com/praveensirvi1212/jenkins_sonarqube_basic_project/blob/main/images/Screenshot%20from%202023-02-16%2015-32-33.png) 
 
You can find your jar file build by maven at /var/lib/jenkins/workspace/devopscicd/target/ this location

Sonarqube Output: 

![](https://github.com/praveensirvi1212/jenkins_sonarqube_basic_project/blob/main/images/Screenshot%20from%202023-02-16%2001-00-34.png) 

Jar file Deploy Output:

![](https://github.com/praveensirvi1212/jenkins_sonarqube_basic_project/blob/main/images/Screenshot%20from%202023-02-16%2015-29-18.png) 
