# Building Jobs Pipeline

## Creating More Jobs to add to pipeline
Lets create 2 more jobs so that we could connect those together to setup a mock build pipeline.

To create new jobs, you could click on create items, name the job and select the last option which says Copy from Another Job.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/21d48b04-0a3b-4084-931a-7614454973fe)

For this tutorial, lets create jobs by name job2 and job3 which should be copies of job1.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/b2056f43-893f-4967-9b7e-e4724917b1be)

At the end of this exercise, you should see 3 jobs listed on jenkins dashboard as above. While creating Job2 and Job3 for the first time, do not use any build triggers. We will update the configurations while defining upstream/downstream.

## Connecting jobs
Lets now create a pipeline by connecting these jobs together. We would create a pipeline with
```
job1 => job2 => job3
```
Where, job2 should run, only if job1 is built successfully, and should trigger job3 once it builds itself successfully. We could either define both connections from job2, or go to job1 and job3 and define its relationship with job2. We would do the later.

Lets open Job1 configurations and from Post Build Actions select Build Other Projects and select job2.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/6c67af4a-eabf-4e14-8ace-ce68ac895075)

Lets also go to jobs3 and define a dependency on job2. To do so, you would have to scroll to Build Triggers section and select Build after other projects are built and provide job2.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/01f7afec-5d10-4b3e-8053-be8ab163a50b)

## Upstreams and Downstreams

Jenkins calls these connections as Upstreams and Downstreams. In the context of job1, its downstream is job2. And for job2, job1 is its upstream. Same goes with job2 and job3. This is depicted in the following image which shows the job2 configurations.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/6bb70b4a-1bf9-46ee-b055-06a940445995)

## Install Pipeline Plugin

To get a better view of the complete pipeline and the workflow, we would install a plugin which allows us to create a special view for connected jobs.

To install this plugin,

From Manage Jenkins select Manage Plugins.

Click on Available tab and start typing "pipeline" int he filter box. No need to press enter.

Check the box against Build Pipeline Plugin, the second option, and click on the button at the bottom to "Download and install after restart".

If you don't see this plugin in the Available list then check the Installed list to see if it is installed already.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/102be6ef-8d35-43e7-a0b9-3d817b60745f)

## Crete Pipeline View
Lets now create a pipeline view.

From Jenkins dashboard click on the + symbol besides the current list view named ALL which displays all jobs.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/5055ba9b-1791-4318-b52a-02ee21d631e5)

Provide a name to the view e.g. pipe1, check the radio button for Build Pipeline View. Click on ok.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/f26a9ff1-6f24-4a1d-8cf6-97e177256047)

From the view configurations, select initial job from the drop down menu and the number of displayed builds. Click on OK to finish configurations and show the view.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/0e997980-d7ba-4d19-be36-33515cfd5b09)

## Run pipelines
The pipeline view reads the first job, and picks up all the jobs which are directly or indirectly connected showing you one single view of the complete workflow and the order in which it is going to be executed.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/e2e7dea7-fa72-4a44-9878-388b33d1c4cd)

Pipeline view also shows the history of job runs up to the number of instances you selected earlier in the configurations.

Go trigger a Run from the pipeline view and see what happens. Make sure you have selected "ENABLE AUTO REFRESH" earlier from the top right corner of the screen.
