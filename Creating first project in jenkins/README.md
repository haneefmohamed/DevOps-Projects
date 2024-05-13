# Creating First Project

We are going to create and launch our first project with jenkins. We will be using a free style project for this example.

# Types of Jobs
With Jenkins you could create following kind of projects or jobs.

Free Style
Maven
External Job
Multi Configuration

# Jenkins Jobs Anatomy
A typical style jenkins jobs has the following sections.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/5b4931ae-d324-48ee-a897-c150f6c621fa)

-Name/description

-Advanced Option

-Source Code Management

-Build Triggers

-Pre Build

-Build

-Post Build

# Creating a Simple Job
Lets now create a simple job using jenkins to run a hello world program.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/d0ef6f95-4954-4631-b3d8-65f1f9e75ffe)

From jenkins main page , click on New Item
Provide a name to the project in Item Name i.e. "job1". Check against Free Style Project.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/bf313468-afa2-4e28-9ab7-a4ac45bdec43)

Next screen opens the job configuration page. On the job configuration page,

Add job description. e.g., "Our first Jenkins Job".

Skip Source Code Management and Build Triggers, and scroll down to Build configurations.

From "Add Build Step" select Execute Shell and provide commands to execute. Since this is a mock job, you could provide following sample code,

```
#!/bin/bash
echo "Hello World !"
sleep 10
```
Review and click on save to go to project page.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/effe3687-769b-4aaa-8a29-13fb974b6571)

# Building Job for the First Time
Click on Build Now to launch a build. Once the build is started, you would see the status in the Build History section.

Once build is finished, click on the build number which starts with # . Clicking on the build number e.g. #1 will take you to the page which shows the build stats. Option of interest on this page might be Console Status which shows the run time output.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/6ba6a1ea-aa72-4cfe-acce-6030e30025cf)

All done !!
