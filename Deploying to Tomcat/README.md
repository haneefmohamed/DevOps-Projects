# Deploying to Tomcat
We have setup the jobs which compile code and then run unit tests, static code analysis etc. Once its been unit tested, we would like to deploy the software. In this case we would deploy it to a tomcat server in our development environment. Later on, we would also create a docker image which could then be either deployed to production, or shipped to the customers.

## Preparing Tomcat for Deployment
### Running Tomcat as a Docker Container
We assume that docker image for Tomcat is being pulled from dockerhub.com

To deploy to tomcat, we first need to create user configurations to enable tomcat admin UI.

Lets create a ```tomcat-users.xml``` in on the docker host machine.

This tomcat-users.xml file contains,

```
<?xml version='1.0' encoding='utf-8'?>

<tomcat-users xmlns="http://tomcat.apache.org/xml"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://tomcat.apache.org/xml tomcat-users.xsd"
              version="1.0">

  <role rolename="admin-gui"/>
  <role rolename="manager-gui"/>
  <user username="admin" password="password" roles="admin-gui,manager-gui,manager-script"/>

</tomcat-users>
```

This file need to be mounted inside the container in ```/usr/local/tomcat/conf/```.

Now use docker run command with port mapping and volume mount option to run Tomcat docker container.

```
docker run -idt -p 8888:8080 -v /path/to/tomcat-users.xml:/usr/local/tomcat/conf/tomcat-users.xml tomcat
```
Replace /path/to/ with the corresponding absolute path of tomcat-users.xml file that you have created.

## Tomcat Configuration in Jenkins
Install Deploy to Container Plugin in jenkins.

Create a project called deploy which is a copy of test job.

But the maven goal should be "package".

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/ce41278c-2be9-4828-b757-793a7a7228e8)

From post build action, select deploy to EAR/WAR Container.

```
context: cmad
tomcat url : http://ipadress:8888
user: admin
pass: s3cret
```
From post build action, select Deploy artifacts to Artifactory.

Refresh to get the target repositories.

Verify browser for Deployment.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/6fa336c8-b3ea-416a-8cd5-03b88e1bf9c3)

