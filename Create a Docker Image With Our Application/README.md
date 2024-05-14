# Create a Docker Image With Our Application
Now our application is ready to be used as a result of successful Package job run. In this chapter, we are going to...

Build a Docker image with our application in it.

### Pre-requisites
(Note: Visit hub.docker.com and create a DockerHub account if you don't have one already.)

### Pre Requisite 1 - Set up Docker Environment for Jenkins
Install CloudBees Docker Build and Publish Plugin

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/4699d75b-76bd-45d0-8fd6-29ecbd3aa03c)

After installing that plugin, go to `Credentials => global(global domain) => Add credentials => fill in the details

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/450a5bba-4490-4e8c-89bf-9da857cbd837)

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/338e2c1a-6378-42c0-ad02-78f411ae8cfb)

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/6c6b158e-7f10-41ac-b29c-0bf7306bec5e)

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/698b3b21-6380-402d-9b68-321d4ecba8ba)

Now go back to Jenkins Main Page
### Pre Requisite 2 - Dockerfile
You should have created a Dockerfile by now which should be part of the application source code.

## Create "Build Docker Image" Job
This time create a freestyle project named Build Docker Image.

In Source Code Management step, add YOUR git repository.
```
eg:
https://github.com/initcron/demo.git
```
[Replace the above with your own repo URI]

In Build Trigger, add the previous job e.g. Static Analysis as a trigger.

Click on apply project for now.

## Build and Publish Docker Image
This job has one Build step.

Select Docker Build and Publish from the Build step

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/728b0393-4ce9-4dea-a426-25ab7f98ddf2)

Add the following details in the fields.

Repository Name (e.g. username/repo)
Tag (e.g. staging)
Docker Host URI : unix:///var/run/docker.sock

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/74d387ca-ad86-4fb2-970b-aed1a5eef519)

Then click on Save.

Now you can run the Docker-Image job

If everything goes well, this job will create a Docker image and push it to DockerHub registry.

