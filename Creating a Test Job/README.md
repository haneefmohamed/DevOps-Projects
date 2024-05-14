# Creating a Test Job
In the previous chapters we have created a build job and have integrated it with git and artifactory. In this chapter, we would create a job which tests the code after its been successfully compiled. We would go on to integrate this with Sonarqube later to do static code analysis.

## Create A Job to run Unit Tests
From New Items create a new project. Name it as Unit Tests and select copy from existing item. Provide "build" as the job name to copy from.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/571dc53c-af3a-423a-ba84-265e63f2c776)

Review Job Configurations

Provide Description.

Check Resolve Artifacts from Artifactory from Build Environment. Provide the same configurations as build job that we configured earlier to connect with artifactory.

Review Build Triggers. Remove polling if present.

From Build Triggers, select Build After Other Projects are Built and provide dependency on "build".

From Build, Select test as Goals and Options.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/c2e9c8b5-e664-4e3a-914b-015a79bec7d0)

Review, Save and Build.

