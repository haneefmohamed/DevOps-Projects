# Installation on EC2 Instance

-Go to AWS Console

-Instances(running)

-Launch instances

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/f049343a-ad71-430b-894c-7f5080441c0b)

# Install Jenkins.

Pre-Requisites
Java (JDK)

# Run the below commands to install Java and Jenkins

Install Java
```
sudo apt update

sudo apt install openjdk-11-jre
```

Verify Java is Installed
```
java -version
```
Now, you can proceed with installing Jenkins
```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
**Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

EC2 > Instances > Click on

In the bottom tabs -> Click on Security

Security groups

Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/d8b2f464-bd1e-4feb-ab51-dcd8d1de637e)

# Login to Jenkins using the below URL:

http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

Note: If you are not interested in allowing All Traffic to your EC2 instance 1. Delete the inbound traffic rule for your instance 2. Edit the inbound traffic rule to only allow custom TCP port 8080

After you login to Jenkins, 
- Run the command to copy the Jenkins Admin Password

- sudo cat /var/lib/jenkins/secrets/initialAdminPassword

- Enter the Administrator password

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/de4d8cc4-4d40-4eff-8264-9d65326088e6)

# Click on Install suggested plugins

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/a2b5f3a8-c525-4e15-973b-735b7754ab7a)

Wait for the Jenkins to Install suggested plugins

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/944c5d4a-2882-4734-a34f-589f3b3000b1)

Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/4bf4a12f-9fef-4875-8af3-f694b0de3449)

Jenkins Installation is Successful. You can now starting using the Jenkins

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/0faa707b-bc38-4cae-8e83-3323a7ba331b)

# Install the Docker Pipeline plugin in Jenkins:
-Log in to Jenkins.

-Go to Manage Jenkins > Manage Plugins.

-In the Available tab, search for "Docker Pipeline".

-Select the plugin and click the Install button.

-Restart Jenkins after the plugin is installed.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/6b02d9bf-16f0-450e-b95b-36abd534325b)

Wait for the Jenkins to be restarted.

# Docker Slave Configuration

Run the below command to Install Docker

```
sudo apt update
sudo apt install docker.io
```
# Grant Jenkins user and Ubuntu user permission to docker deamon.

```
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```
Once you are done with the above steps, it is better to restart Jenkins.

```
http://<ec2-instance-public-ip>:8080/restart
```
The docker agent configuration is now successful.

That's it ! 
All done !
