# DevSecOps-project

In this project, I created an end-to-end CI/CD pipeline while keeping in mind Securities Best Practices, DevSecOps principles and used all these tools *Git, GitHub , Jenkins,Maven, Junit, SonarQube, Docker, Trivy, AWS S3, Docker Hub, Kubernetes , Slack and Hashicorp Vault,*  to achive the goal.


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

## Want to create this Project by your own  then *Follow these  project steps*

### Stage-01 : Install JDK and Create a Java Springboot application
Push all the web application page code file into github

![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/code.png) 

### Stage-02 : Install Jenkins and start Jenkins 
1. Installation guide is available here  https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Jenkins_installation.md
1. After installation, install suggested plugins
1. Open Jenkins Dashboard and install required plugins – SonarQube Scanner, Hashicorp Vault, Slack
1. go to manage jenkins > manage pulgins > search for plugins > install without restart
![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/jenkins.png) 

1. We will required another pulgin called - Kubernetes Continuous Deploy Plugin ( this plugin is deprecated but we can down grade the version for just testing purpose)
Download the Plugin file from here https://github.com/praveensirvi1212/DevSecOps-project/blob/main/kubernetes-cd.hpi
1. Now go to manage jenkins > manage pulgins > Advanced Setting > Deploy Plugin > choose the download file ( kubernetes-cd.hpi) > click on Deploy
![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/plugins.png) 

### Stage-03 : Install Postgre Database and Install SonarQube
1. Installation guide is available here https://github.com/praveensirvi1212/DevSecOps-project/blob/main/sonarqube_installation_with_postgres_database.md
![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/sonarqube.jpeg) 
### Stage-04 : Install Docker and Create DockerHub account
1. Installation guide is available here https://github.com/praveensirvi1212/DevSecOps-project/blob/main/docker_installation.md
1. Create DockerHub account 

![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/dockerhub.png) 


### Stage-05 : Install Trivy for Vulnerability Scanner for Containers and other Artifacts
I am following  Debian/Ubuntu  based installation guide you can choose accourding to your os

```sh 
   sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
   ``` 
#### After trivy installation you can scan Container Images, FileSystem, Git Repositories
In our can we will scan contianer images

```sh 
   trivy image [YOUR_IMAGE_NAME]
   ``` 

### Stage-06 : Install Hashicorp Vault server 
HashiCorp Vault is a secret-management tool specifically designed to control access to sensitive credentials in a low-trust environment.
1. Installation guide is available here https://www.cyberithub.com/how-to-install-hashicorp-vault-on-ubuntu-20-04-lts/

### Stage-07 : Install Slack
Slack is a workplace communication tool, “a single place for messaging, tools and files.” .

Install Slack from official website of Slack https://slack.com/intl/en-in/downloads/linux


### Stage-08: Install Minikube
Minikube installation Guide is Available here  https://www.linuxtechi.com/how-to-install-minikube-on-ubuntu/

# Done with Installation , Now will we integrate all the tools with Jenkins
### Stage-01 : Hashicorp Vault integration with Jenkins
I am assuming that your Vault server is running 

Video guide to integrate Hashicorp Vault with Jnekins https://www.youtube.com/watch?v=5-RMu9M_Anc

##### 1. create Vault server App role and secret id 
* Copy the following to `/etc/vault.d/vault.hcl`
```
storage "raft" {
  path    = "/opt/vault/data"
  node_id = "raft_node_1"
}

listener "tcp" {
  address     = "0.0.0.0:8200"
  tls_disable = 1
}

api_addr = "http://127.0.0.1:8200"
cluster_addr = "https://127.0.0.1:8201"
ui = true
```

* `sudo systemctl stop vault`
* `sudo systemctl start vault`

#### Commands to run to configure Vault and create AppRole

* `export VAULT_ADDR='http://127.0.0.1:8200'`
* `vault operator init`
* `vault operator unseal`
* `vault operator unseal`
* `vault operator unseal`
* `vault login <Initial_Root_Token>`
   * `<Initial_Root_Token>` is found in the output of `vault operator init`
* `vault auth enable approle`
* `vault auth enable approle`
  * https://www.vaultproject.io/docs/auth/approle
* `vault write auth/approle/role/jenkins-role token_num_uses=0 secret_id_num_uses=0 policies="jenkins"`
* `vault read auth/approle/role/jenkins-role/role-id`
	* copy the role_id and store somewhere
* `vault write -f auth/approle/role/jenkins-role/secret-id`

##### 2. Now go to jenkins > Manage  Jenkins >Manage Credentials > system > Add credentials > Vault App Role Credentials > paste roleid and secret id token we create in Vault and save and apply.
![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/approleVault.png) 


 ### Stage-02: SonarQube integration with Jenkins
1. Open SonarQube and login using admin username and admin password
1. Create a Project >Enter Project name, Project key > click on setup
![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/sonarqubedb.png)
1. Create sonarqube token > and save it soemwhere
1. click on continue > Run analysis on your project > maven > copy following commands and save it some where
![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/soanr.png)
1. Now go to jenkins >Manage Credentials > system > Add credentials > secret text file > paste token we create in sonarqube and save and apply.

1. go to manage Jenkins > Configure System > Add SonarQube Server name,url and credentials
![](https://github.com/praveensirvi1212/DevSecOps-project/blob/main/Images/sonarqube.png)
1. go to manage Jenkins > Global tool configuration >  Add Maven and SonarQube Scanner


### Stage-03 : Add jenkins user to docker group
 ```sh 
sudo gpasswd -a jenkins docker
 ``` 
### Stage-04: Install and Configure AWS CLI
 1.Installation Guide is Available here https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html 
1. go to AWS > create access key and secret key
1. configure aws cli using
```sh 
aws configure
 ``` 
paste your  access key and secret key 
#### Method 1
configure aws cli for jenkins user also 

##### Note – in this project i used  method 1 but you can also use method 2

#### Method 2 
1. go to jenkins > Manage Credentials > system > Add credentials > AWS credentials > give your access key and secret key > save

Pipeline Syntax 
```sh 
stage("Upload"){
steps{
withAWS(region:"${region}", credentials:"${aws_credential}){
s3Upload(file:"${TAG_NAME}", bucket:"${bucket}", path:"${TAG_NAME}/")
} 
}
 ``` 
