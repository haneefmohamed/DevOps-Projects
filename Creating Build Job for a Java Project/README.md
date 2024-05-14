# Creating Build Job for a Java Project
In this chapter, we are going to create a job to build/compile a sample java application with maven.

## Creating Maven Project
Before we start to create our build job, we need to install maven-integration plugin.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/a6ed5d8b-7298-4a0e-b56f-7c43383b788e)

To create a build project,

From New Item, select Maven Project and provide it a name e.g. "build".
Note: If you do not see Maven Project option on the job creation page, install Maven Integration Plugin from plugins manager.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/89bfcc27-a94b-4357-9c9c-f5e3dd13d2ec)

From the configuration screen, scroll to Source Code Management, select GIT and provide repository URL

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/857ee792-4ad5-4b3d-8f02-4627c66f7e7c)

From Build Triggers select Poll SCM. Lets configure it to poll every 5 minutes using the following schedule

```
H/2 * * * *
```
![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/fcdc0eee-8d96-40a5-a2be-df31af12e36c)

Scroll down to Build step and you should see Root POM selected since its a Maven Project. In the Goals and options section, provide compile as a goal.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/48077859-e5d0-4a95-86b4-5633d903f720)

In addition to compile, following are the goals Maven project could take.

validate

compile - compile source code

test - unit tests

package - build jar/war

integration-test

verify

install

deploy

Save the job and click on Build Now. Following is a snippet from the output of the build job.

```
[INFO] Compiling 1 source file to /var/jenkins_home/workspace/build/target/classes
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 10.216 s
[INFO] Finished at: 2016-04-27T17:11:30+00:00
[INFO] Final Memory: 19M/240M
[INFO] ------------------------------------------------------------------------
Waiting for Jenkins to finish collecting data
[JENKINS] Archiving /var/jenkins_home/workspace/build/pom.xml to com.example.app/maven-app/3.0-release/maven-app-3.0-release.pom
channel stopped
Finished: SUCCESS
```
