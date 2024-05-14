# Creating a Package jobs
In the previous chapter, we have learnt about SonarQube. In this chapter, we will learn about how to package our application.

Just like other maven jobs, Create a new job called Package, which is a copy of test job, and click on OK.

Then, Change the Build trigger to Build after other projects are built. This project should be built after **SonarQube Static Code Analysis Job.**

In the Build step, set package -Dmaven.test.skip=true as the maven goal.

The most important step in this chapter is the Post-build Action.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/2370cf6f-30ba-40d9-a039-bf330bc7f901)

Select Archive the artifacts from the drop down menu.

In Files to archive section, set *target/.war* as a value.
