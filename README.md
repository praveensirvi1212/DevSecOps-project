# DevSecOps-project

In this project, In this Project I created an end-to-end CI/CD pipeline while keeping in mind Securities Best Practices, DevSecOps principles and used all these tools *Git, GitHub , Jenkins,Maven, Junit, SonarQube, Docker, Trivy, AWS S3, Docker Hub, Kubernetes , Slack and Hashicorp Vault.*  to achive the goal.


## Project Architecture
![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/architecture.png)

### PreRequisites
1. JDK 
1. Git 
1. Github
1. Jenkins
1. Sonarqube
1. Docker
1. Trivy
1. AWS account
1. Docker Hub account
1. Minikube & Kubectl
1. Hashicorp Vault
1. Slack

### Stage-01 : Install JDK and Create a Java Springboot application
Push all the web application page code file into github

![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/code.png) 

### Stage-02 : Install Jenkins and start Jenkins 
1. Installation guide is available here  https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Jenkins_installation.md
1. After installation insatll suggested plugins
1. Open Jenkins Dashboard and install required plugins – SonarQube Scanner, Hashicorp Vault, Slack
1. go to manage jenkins > manage pulgins > search for plugins > install without restart
![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/jenkins.png) 

1. We will required another pulgin called - Kubernetes Continuous Deploy Plugin ( this plugin is deprecated but we can down grade the version for just testing purpose)
Download the Plugin file from here https://github.com/praveensirvi1212/DevSecOps-project/blob/main/kubernetes-cd.hpi
1. Now go to manage jenkins > manage pulgins > Advanced Setting > Deploy Plugin > choose the download file ( kubernetes-cd.hpi) > click on Deploy
![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/plugins.png) 

