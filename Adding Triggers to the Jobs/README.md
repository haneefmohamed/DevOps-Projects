# Adding Triggers to the Jobs

## Build Triggers
Build triggers decide when a jenkins job is run. Whether it happens based on a external event e.g. a push to git repository, a scheduled run, or a job is run after another job is completed, there are plenty of options to trigger builds.

From project page, click on Configure.

## Types of Triggers

1.Trigger builds remotely

2.Build after other projects are built

3.Build periodically

4.Poll SCM

## Execute Jobs Remotely

Jobs can be triggered remotely outside of jenkins. This is very useful when you would like the jobs to be triggered based on some event or part of the logic you have written as part of your script. This is also the way you would trigger the job based on the activities performed on the repositories. e.g. adding new commit to git hub.

Example:
Click on job1 and then select Confgure

In Build Trigger, check Trigger Builds remotely.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/8b8a2e69-e992-48ca-8e2c-193fe0c4a00c)

Define a token (More complex one than the example)

Save the job.

To trigger the job, you need two things

user
user's API token
We will use admin (first user we created) user's API token to trigger this job. You can find this at
```
jenkins_homepage -> people -> admin -> configure
```
![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/8e86670a-2d37-4667-8cff-b7fefa6d901b)

Click on Show API Token Note down the user's API token.

Visit the trigger from browser or use curl

```
user:<API_TOKEN>@<Jenkins_URL>/job/job1/build?token=<JOB_TOKEN>
Example: http://admin:552dab89b070c0fcc3fad281c51318ad@10.40.1.14:8080/job/job1/build?token=mytoken
```
This will trigger the build.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/43e952f0-a0b7-4966-9abc-2d9d5b1624c5)

## Building Jobs Pipeline
One of the important features of Jenkins is its ability to build a pipeline of jobs, whereas based on the outcome of one job, another can be triggered. e.g. only if you are able to compile the code, you may want to proceed with testing, else its quiet useless to do so. Using Build after other projects are built trigger, this can be easily achieved. We will be creating a job pipeline using this feature in the next chapter.

## Scheduled Runs
Similar to creating cronjobs or scheduled jobs its possible to define a run time schedule with jenkins.

## Polling SCM
This option allows jenkins to regularly check the source code management system e.g. a remote git repository to check if there are any updates, and launch a job based on it. Ideally post commit hooks/webhooks with git should trigger the builds, howeever it may not always be possible. E.g. if you are hosting jenkins inside a private network, which is not reachable by git repository hosted on the cloud, triggering a webhook will not be possible. In such cases the next best option is to poll git repository at a regular interval and trigger the builds.
