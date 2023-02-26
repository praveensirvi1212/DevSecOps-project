#Step 1 - Install Java on Ubuntu 22.04
```sh 
   sudo apt install openjdk-11-jdk
   java -version
   ```
#Step 2 — Installing Jenkins
```sh 
   wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key |sudo gpg --dearmor -o /usr/share/keyrings/jenkins.gpg 
   sudo sh -c 'echo deb [signed-by=/usr/share/keyrings/jenkins.gpg] http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
   sudo apt update
   sudo apt install jenkins
   ```
#Step 3 — Starting Jenkins
```sh 
   sudo systemctl start jenkins.service
   sudo systemctl status jenkins
   ```
#Step 4 — Opening the Firewall   
```sh 
   sudo ufw allow 8080
   sudo ufw allow OpenSSH
   sudo ufw enable
   ```
 #Step 5 — Setting Up Jenkins
   To set up your installation, visit Jenkins on its default port, 8080, using your server domain name or IP address: http://your_server_ip_or_domain:8080
You should receive the Unlock Jenkins screen, which displays the location of the initial password:


   ```sh 
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   ```
  
Copy the 32-character alphanumeric password from the terminal and paste it into the Administrator password field, then click Continue.
