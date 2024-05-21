# Complete Step-by-Step Jenkins CICD with GitHub Integration
## Overview
CI/CD is a method to frequently deliver apps to customers by introducing automation into the stages of app development. The main concepts attributed to CI/CD are continuous integration, continuous delivery, and continuous deployment.

Therefore, CI/CD has been the main component of the software development cycle, with so many configurations and tools available. We will use Amazon Web Services (AWS) as the cloud platform, GitHub for the code repository, Jenkins for the Continuous Integration (CI), and Continuous Delivery (CD).

## Requirements:

-AWS account.

-Jenkins and Docker are to be installed on the AWS EC2 Instance

-GitHub repo (code)

### Step 1: Setup AWS EC2 Instance
We will first create an AWS Instance (Ubuntu) free-tier eligible using the AWS console.

Steps To launch the EC2 instance:
Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.
Choose Launch Instance.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/a4deaa18-c82d-4a8f-9671-27868c1de73d)

Once the Launch an instance window opens, provide the name of your EC2 Instance:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/8fcefff1-069b-43ec-9460-bdb402339c96)

Choose the Ubuntu Image (AMI):

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/b9f0a194-b135-4efd-a9dc-0cc914dafb20)

Choose an Instance Type. Select t2.micro for our use case which is also free-tier eligible.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/a9258258-7626-4f22-aab4-d4a438a4be76)

Select an already existing key pair or create a new key pair. In my case, I will select an existing key pair.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/6b5c5b2f-9d32-46d5-9f21-3eb06800a3e1)

Edit the Network Settings, Create a new Security Group, and select the default VPC with Auto-assign public IP in enable mode. Name your security group and allow ssh traffic, HTTPS, and HTTP from anywhere (later on we can modify the rules)

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/23f6e539-6d6d-4c12-89bb-b3740a2d977b)

 Leave the rest of the options as default and click on the Launch instance button:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/e43a9bbe-96d5-41d3-9014-456c750d47d5)

On the screen you can see a success message after the successful creation of the EC2 instance, click on Connect to instance button:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/86888155-d900-42c3-b468-39336f9078bf)

Now connect to instance wizard will open, go to SSH client tab and copy the provided chmod and SSH command:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/476c5220-84e5-4b0f-ae3b-f5959112d3a3)

Open the Command Prompt or PowerShell in your local machine and paste the following two commands and you will be able to access your EC2 machine:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/23829767-aee6-42b4-a1fb-c4339e963da0)


### Step 2: Install Jenkins on EC2 Instance:
Jenkins installation is straightforward:

1.First Update your Server with the command
  ```
 $  sudo apt-get update
```
2. Install Java
```
 $ sudo apt install openjdk-11-jre
```
3. Verify Java Installation:
```
 $ java -version
```
It should look something like this
```
openjdk version “11.0.12” 2021–07–20 OpenJDK Runtime Environment (build 11.0.12+7-post-Debian-2) OpenJDK 64-Bit Server VM (build 11.0.12+7-post-Debian-2, mixed mode, sharing)
```
4. Install Jenkins:
Just copy these commands and paste them onto your terminal.
```
          $ curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
          $ echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \   https://pkg.jenkins.io/debian binary/ | sudo tee \   /etc/apt/sources.list.d/jenkins.list > /dev/null
          $ sudo apt-get update
          $ sudo apt-get install jenkins
```
5. Start Jenkins:
```
          $ sudo systemctl enable jenkins
          $ sudo systemctl start jenkins
          $ sudo systemctl status jenkins
```
With these changes, our Jenkins Server should be installed on our EC2 Server. Before we access our Jenkins Server on our browser, let's open the default TCP port 8080 under the Security Group of your Instance and allow MYIP only to access the Server.
For security purposes, I hid my IP.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/1f43a5ba-5e38-47b5-a9ef-33a00b6b8935)

To verify the installation of Jenkins we can take the public IP of our EC2 Instance and paste it into our browser with a default port of Jenkins 8080.
Then the Jenkins Page would appear as below:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/4e347e3f-eefd-4864-b1dc-17952533893c)

Now to unlock Jenkins we need to go to this path /var/lib/jenkins/secrets/initialAdminPassword and copy the administrative password and paste it into the above screenshot.

After pasting the password the below page will appear. Click on Install suggested plugins.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/52194deb-fc6b-4e2f-bdbd-4722e67b66f5)

After the plugins are installed, you need to create the first Admin User. Fill in all the information and click on Save and Continue.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/2aa514b3-93e3-425e-a480-bb5802da60ae)

Then the wizard will display the Jenkins URL through which you will be able to access the Jenkins Server. Click on Save and Finish and start using Jenkins.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/e6101bf6-f3c6-417d-bc2b-8a50fb8daa89)

### Step 3: Start Using Jenkins:
On Jenkins Dashboard, Click on New Item to create your first job or item.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/eb5f14dc-3cc7-4c89-9e6f-fe43cab00414)

Enter the name of your first item and select Freestyle Project and click on Ok.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/7172190f-a38e-4024-9413-8c0946e4840f)

Now we need to configure various parameters of our first job in Jenkins. Under the General section, put the description of your project. Under Project Url paste the GitHub URL of the project for which we need to create the CI CD Pipeline.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/39ecf5a8-1170-4d17-b434-e4a6591cb9cb)

Under Source Code Management we need to paste the GitHub repository URL as shown in the below screenshot:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/31c5f018-95a4-4f06-972f-abb3d7592be8)

Under credentials, we first need to generate the ssh keys on our EC2 Server.
The reason to create ssh keys is to make secure integration between our Jenkins Server and Github and this way we can clone any git repo in this Jenkins instance. You do not need to provide the credentials while configuring the job in Jenkins.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/9c63863c-70bf-4ccd-904c-e6cdafee92e5)

Take the public key and insert that under the settings in GitHub to achieve a password-less connection between Jenkins and GitHub.

For that go to the settings of your GitHub, on the left choose SSH and GPG keys, click on New SSH key, give the name under Title, and paste the public key under the Key section we previously generated on the EC2 server.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/26369c6e-bdf3-4339-8de9-5915c070478a)

After adding the ssh key to our GitHub account we will add the credentials in Jenkins. For that, under credentials click on Add button and click on Jenkins in the drop-down option.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/bc0ffc68-bdc4-4246-9de4-fe36f88a54b5)

A new window will appear. Select SSH Username with private key under the section Kind. Give any name under section ID and Description, as shown in the below screenshot:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/d7c05724-4abc-4d61-8fb8-15f51a18da3c)

On the other half of this page type the Username of the EC2 machine which in our case is ubuntu and then paste the private ssh key copied from your EC2 server and click on Add button.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/0065bf12-e629-499e-b589-814ac1c9a620)

Now we have to specify the branch of our GitHub repository. It can be any branch the developer would have been working on. In our case, we will select the master branch.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/9601d32f-5049-4818-b364-d4cd89c33275)

This is all we need so far as the configuration of our first job is concerned. We can save this part of the configuration and move to the next step of building the project.

To check whether our GitHub integration with Jenkins is successful we will do a small test by clicking on Build Now on the left navigation bar in our first job as shown below:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/ea941d0c-7d54-4ed7-9522-8fb707050825)

After clicking on Build Now we see in the output console that the build has been finished successfully and Jenkins was able to fetch the code from our GitHub repository. That means Jenkins Integration with GitHub is successful.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/99a19f00-ceb9-4002-a681-5e4611c72015)

We can also verify by navigating to the path mentioned in the output console which is:
```
              /var/lib/jenkins/workspace/todo-node-app
```
And check if the repo is cloned there. As shown in the below screenshot we see all the files of the GitHub repo have been successfully cloned.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/66121da7-5b2d-4c1f-876f-87e05c33d227)

### Step 4: Run the code:
To run the code we will go through the steps provided by the developer in the Readme file of the Repo which is as shown below:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/bc1631b5-56f6-48d1-b9f0-e01c243b70e8)

Let’s run these commands on the EC2 Instance one by one:
```
                  $ sudo apt install nodejs
```
Output:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/06a05779-a494-4d37-8f27-75c1c6be3ee1)
```
 $ sudo apt install npm
```
Output:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/050ef0f1-30e4-49b1-a5f9-2051b42699b4)

```
 $ npm install
```
The above command will install the dependencies mentioned in the file package.json (ignore the warnings in the output)

Output:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/0a4560fb-d9fd-4622-bb7a-29d8122557a4)

Finally, to run the app we need to execute the final command, however, before that we also need to allow port 8000 in the Security group of our EC2 Instance as this app will be running on port 8000.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/395b9276-36d7-491e-8561-4bf94b940fe3)

After allowing port 8000 in the inbound policy of Security Group we will run the final command as:
```
                          $ node app.js
```
To check the output open your browser take the public IP of your EC2 Instance with port 8000 and you will see the result as:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/1b56b200-15ed-41a7-ab70-c00f60649a62)

At this point, we are running the app on our Server and if we stop our service the app will be no longer available to others so for the app to be accessible anywhere by anyone we need to dockerize the application.

### Step 5: Install Docker on EC2 Instance:
Install Docker with the following command:
            ```
            $ sudo apt install docker.io
            ```

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/e7efbe28-f66a-4aaf-8650-d27091ebc2a8)

Create your Dockerfile:
We will create the Dockerfile in the same directory /var/lib/jenkins/workspace/todo-node-app
```
FROM node:12.2.0-alpine
WORKDIR app
COPY . .
RUN npm install
EXPOSE 8000
CMD ["node", "app.js"]
```
Now we will build the Image using the Dockerfile created in the above step:
```
              $ docker build . -t todo-node-app
```
In the below output watch the build steps which match with the instructions in the Dockerfile:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/1b7ddefd-0550-4841-b02e-6c1e9a751883)

We have successfully built the Image from the Dockerfile:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/908a1a35-6bd8-469a-a2ab-ee80af9f9b9f)

Now its time to build the container from the same Image
```
          $ docker run -d --name node-todo-app -p 8000:8000 todo-node-app
```
![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/cbc68f48-d967-4e59-ac54-7d119ff4cd3f)

We can verify the successful creation of the container with the below command:
```
                      $ docker ps
```
![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/f8502c4f-ed9f-4ff7-88f7-52c155ed52c4)

Also, we can test by accessing it on our browser as well:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/05cc4c38-5426-4e09-9d7e-d4650ea181b9)

Up until here, we saw how to dockerize the app manually and make it available for everyone to access.

### Step 6: Using Jenkins to Automate the whole process
In Jenkins, we will use all the commands we ran earlier to build the docker Image and then build the container from that image.
For that go under the Build Steps section of Jenkins configure settings of our job and add the following commands in the execute shell area:
```
     docker build . -t todo-node-app
     docker run -d --name node-todo-app -p 8000:8000 todo-node-app
```
Once you add the commands click on the Save button as shown in the below screenshot:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/a3f7ad56-2257-42bd-ad66-60b356046512)

Now Click on Build Now to build the job using Jenkins.

After you click on Build Now you may encounter an error in your build as shown in the below screenshot:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/4bbe9da3-95d1-47f5-ae1b-be69ba627a25)

To solve this run the below commands in the EC2 Server which adds the Jenkins user to the docker group and restarts the Jenkins server.
```
              $ sudo usermod -aG docker jenkins
              $ sudo systemctl restart jenkins
```
![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/cb67a05d-daa2-4583-920c-e48f7c54d906)

After the Jenkins Server restarts, again run the Build Now and check the Output:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/7a2fc031-569e-42f8-bc26-a4a4e8d474a2)

This time around our build is successful and we can see our app accessible from the browser.

Now to fully automate this CI CD pipeline without us clicking on Build Now every time the developer makes any changes in the code we will configure a web-hook that will allow our Jenkins job to be automatically triggered whenever it detects any change in the code and thus perform the necessary steps to keep the app up and running with the latest updates.

### Step 7: Configure Web-hook:
To configure the web hook we first need to kill the docker container running on our EC2 Instance by issuing the docker kill “container-id” command.

After that, we will install the GitHub Integration plugin in our Jenkins Server

Jenkins -> Manage Jenkins -> Manage Plugins -> Install github integration plugin

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/366cc644-c85d-4b64-8e71-860ef3942b27)

After adding the plugin we need to add the webhook in our GitHub repo as shown in the screenshot:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/53d0a76d-84bb-465d-a03e-3bb5dc5db470)

A new window will appear where first add the Payload URL which will be the URL through which you access your Jenkins Server with the addition of github-webhook keyword.
The content type should be application/json, the rest should be kept at default and then click on Add webhook.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/2638b8f1-e4a1-486c-a268-cfd74f117924)

The green tick before the Payload URL indicates that the webhook has been successfully configured with Jenkins as shown below:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/37b218a8-e59e-4f63-8440-8d0f64ddecf3)

Now we need to go to the Configure Settings of our Jenkins first Job and select GitHub hook trigger for GITScm polling under Build Triggers and click on Save.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/a100fab8-f4c8-4124-8b7e-d9290270a35a)

Now we will update something in our GitHub repo and our job should get triggered automatically in Jenkins.

The moment I changed something in the code the build got triggered in our Jenkins Job.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/244a4e92-baa5-45cd-926b-eef8d5d84389)

If we check the status of our job it shows that the build got started by GitHub push as shown in the below screenshot:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/f939fe68-e6cc-4a22-9b1f-5ee43349e61b)

And you can also check by typing the URL in the browser to see the changes as follows:

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/09634a1b-1cc1-4396-ab83-7b64953593bb)

Hence we have successfully built the Jenkins CI CD pipeline with GitHub Integration.
