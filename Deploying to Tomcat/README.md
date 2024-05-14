# Deploying to Tomcat
We have setup the jobs which compile code and then run unit tests, static code analysis etc. Once its been unit tested, we would like to deploy the software. In this case we would deploy it to a tomcat server in our development environment. Later on, we would also create a docker image which could then be either deployed to production, or shipped to the customers.

## Preparing Tomcat for Deployment
### Running Tomcat as a Docker Container
We assume that docker image for Tomcat is being pulled from ^dockerhub.com^

To deploy to tomcat, we first need to create user configurations to enable tomcat admin UI.

Lets create a tomcat-users.xml in on the docker host machine.

This tomcat-users.xml file contains,
