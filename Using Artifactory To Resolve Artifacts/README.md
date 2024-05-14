# Using Artifactory To Resolve Artifacts
## Introduction to Artifactory
Following video explains the usefulness of Artifactory to share libraries and artifacts in a collaborated development.
In addition, Artifactory could be used as a local repository for storing rpms, debs, docker images, gems, pythong packages etc.

## Running Artifactory as a Docker Container
We assume that docker image for open source artifactory is being pulled from jfrog.com.

Now use docker run command with port mapping to run artifatcory docker container.

```
docker run -idt --name artifactory -p 8081:8081 docker.bintray.io/jfrog/artifactory-oss
```
Artifactory should come up on the following URL.

http://ARTIFACTORY_URL:8081/artifactory
```
Default Credentials:
username : admin
password : password  
```
After loggin in you will be welcomed with this page.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/1c6d97f6-b88e-4338-a294-f8b24d890b45)

Click on next, You will be asked to set up admin username and password. Skip this for now and use the default credentials.

After that, you will be asked to Configure a Proxy Server. Skip this step as well.

In Create Repositories page, click on maven and click on Create.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/709a199f-988e-4450-8cb3-3630e7021824)

Then click on finish.

## Integrating Artifactory with Jenkins
Artifactory could be used for two purposes,

1.Resolving Libraries/Packages ```From.```

2.Pushing build artifacts ```To.```

In this chapter, we are going to start using Artifactory as a local repository to resolve libraries from. In order to connect Artifactory with Jenkins, first step is to install the Plugin.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/8cf25e7c-9683-4973-bdba-d280eb27d756)

From Manage Plugins, lets filter by "Artifactory", select the relevant plugin and install it. Following is a screenshot of the Artifactory console.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/348e6731-8e16-46b9-a56c-c625a1f8fe6c)

## Configure Artifactory Plugin
Manage Jenkins -> Configure System -> Artifactory -> Add

Add Artifactory details and Test Connection.

e.g.
```
url: http://HOSTNAME:8081/artifactory  
port: 8081  
user: admin  
pass: password  
```

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/0a8f2ea8-f5fb-445e-97e9-ac2964dd8c3a)

Once connection test to Artifactory server is successful, save the configuration page and go back to the main page.

## Resolve Artifacts from Artifactory
Configure build job, and from build environment select Resolve artifacts from Artifactory. Click on Refresh Repositories which should auto select repositories. For snapshots, use libs-snapshot as repo name.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/d6acc480-24e9-4f0b-a4d9-b49b5290f50c)

Validate that the artifacts are being resolved from Artifactory by running a new build and checking the console output.
```
[output snippet]

[INFO] Downloaded: http://52.39.130.66:8081/artifactory/libs-release/org/apache/maven/plugins/maven-plugins/23/maven-plugins-23.pom (0 B at 0.0 KB/sec)
[INFO] Downloading: http://52.39.130.66:8081/artifactory/libs-release/org/apache/maven/maven-parent/22/maven-parent-22.pom
[INFO] Downloaded: http://52.39.130.66:8081/artifactory/libs-release/org/apache/maven/maven-parent/22/maven-parent-22.pom (0 B at 0.0 KB/sec)
```

