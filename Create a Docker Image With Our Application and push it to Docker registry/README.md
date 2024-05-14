# Create a Docker Image With Our Application
Now our application is ready to be used as a result of successful Package job run. In this chapter, we are going to...

Copy the artifact from the package job
Build a Docker image with our application in it.
## Pre-requisites
(Note: Visit hub.docker.com and create a DockerHub account if you don't have one already.)

### Prequisite 1 - Install Copy Artifacts Plugin
Before creating this job, please install copy artifacts plugin which is also a prerequisite.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/eed8c47f-b9a9-4d1b-89af-563ed323e213)

### Requisite 2 - Install CloudBees Docker Plugin
Install CloudBees Docker Build and Publish Plugin

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/d93ce2ec-33dc-487c-b24e-f3027f8ba3a8)

### Requisite 3 - Set up Docker Environment for Jenkins
After installing that plugin, go to `Credentials => global(global domain) => Add credentials => fill in the details

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/e742fabd-a93a-463b-8220-bd7a11b5e370)

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/e0bf8603-0564-478a-8b33-e6069fffe83f)

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/42874926-0920-4d49-998a-c867542d5f49)

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/64f10452-2428-437c-ba35-a745a5b4b4ab)

Now go back to Jenkins Main Page

### Requisite 4 - Fork the docker repository
Fork the following repository.
```
https://github.com/initcron/CI-Vertx.git
```
This repository consists of one **Dockerfile** which you need to update.

Let us see what this Dockerfile does,

### Requisite 5 - The Dockerfile
The Dockerfile is very simple and has only three steps.
```
FROM tomcat:latest
ADD target/CMADSession*.war /usr/local/tomcat/webapps/cmad.war
ADD setenv.sh /usr/local/tomcat/bin/setenv.sh
```
```Line 1```

```
FROM tomcat:latest
```
We are building our image with official tomcat image as a Base image.

```Line 2```
```
ADD CMADSession*.war.war /usr/local/tomcat/webapps/cmad.war
```
Here we copy our application from the host to container.

```Line 3```
```
ADD setenv.sh /usr/local/tomcat/bin/setenv.sh
```
Like the previous step, we add a script inside the image. The purpose of this script is to decrease the launch time of the application. The script has following contents.
```
# Fast up the server boot process
export JAVA_OPTS="$JAVA_OPTS -Djava.security.egd=file:/dev/./urandom"
```
## Docker-Image Job
This time create a freestyle project named Docker-Image.

In Source Code Management step, add the following git repository.
```
https://github.com/initcron/CI-Vertx.git
```
In Build Trigger, add Package as a trigger.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/1a97c866-e04b-45ee-955b-8d69a9708d39)

Click on apply project for now.
## Build Environment
![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/2e6d69ec-6450-463e-913e-b9c1ec5e2e3f)

This job requires workspace to be cleared before it runs. So,

In Build Environment step, Select Delete workspace before build starts then click on Advanced.

In Patterns for files to be deleted section, click on Add.

In the second field add *target/*.war* as a pattern.

## Copy the artifact from Package

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/9f9d32d7-fe24-4fb4-af4b-e7e562fd3cad)

In Build Step, Copy artifacts from another project from the drop down list.

In Project name, Type Package.

Select Latest successful build in the next section.

In artifacts to copy section, type target/*.war

This will copy our application from Package job to Docker-Image job.

## Let's Build the Image
This job has one Build step.

Select Docker Build and Publish from the Build step

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/6d7a8cc3-1bfe-40df-a43e-cb6f698d589c)

Add the following details in the fields.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/58807355-c5df-4a52-b236-d806e5cd44e5)

Then click on Save.

Now you can run the Docker-Image job

If everything goes well, this job will create a Docker image and push it to DockerHub registry.
