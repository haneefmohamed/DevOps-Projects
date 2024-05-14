# Preparing to build Java Projects
After building a pipeline with mock jobs, we are going to start creating a workflow with a real code. And we will select a java project which gets built with Maven, a java based build tool. Running java builds with maven would require additional preparations. Maven should be installed and available on the Jenkins hosts along with the JDK. Lets Install JDK and Maven from the Jenkins dashboard.

## Configure JDK
### Option 1: Configuring Existing OpenJDk
From Manage Jenkins select Global Tool Configuration.

Scroll down to JDK section and click on JDK Installations. Provide a name to the instance of java e.g. "OpenJDK 8".

Uncheck Install Automatically

Provide JAVA_HOME
e.g.
/usr/lib/jvm/java-8-openjdk-amd64

(make sure there is no preceding blank space in above path, when you paste it on jenkins)

If you would like to find the exact value of JAVA_HOME, login to the Jenkins host and run any of the the following commands

```
echo $JAVA_HOME
env | grep -i java
```
![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/90fa96c0-d17d-4171-9bff-5920144b819f)

### Option 2: Installing Oracle Java
[Note: You could skip this, if you have used Option1 above]

If you don't have a existing JDK setup, you can install it from Jenkins itself.

From Manage Jenkins select Configure System.

Scroll down to JDK section and click on JDK Installations. Provide a name to the instance of java e.g. "JDK 8".

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/8b1eda91-4a08-4d88-8bac-67fec6ab4361)

Check the box which mentions "Install Automatically".

From "Install from java.sun.com", select the Version of java that you wish to be installed.

Accept License and click on option to provide Oracle Account credentials.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/5d289e24-82bd-49ff-b13f-3773b46c21eb)

You would have to create a Oracle account, add credentials (email/pass) and have the license accepted in order for JDK to be installed on behalf of you by Jenkins.

Click on Apply button to save the configurations and continue with the next configurations on the same screen.

## Configure Maven
Maven configurations are similar to JDK above, its actually simpler than JDK.

To have Maven installed automatically,

Click on Maven Installations from the Jenkins Systems Configurations page.

Provide a name to the instance of maven being installed e.g. "Maven 3.3.9".

Check "Install automatically" box. Click on save.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/1d59f6b9-4bf4-44bc-90a6-2b6b94f03abd)

Thats it. Maven and JDK will automatically be installed when you create a project with java build.

Note: JDK and Maven are not immediately Installed after providing these configurations. Jenkins would call the procedures to install these when you create a Job which uses JDK/Maven.

