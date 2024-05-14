# Deploy to Staging with Docker-Compose
In the previous chapter we have created our Docker image and pushed it to the Dockerhub registry. Now, we will deploy our application using docker-compose.

## Pre-requisite
### Docker-Compose file Edit
Then fork the following Git repository.
```
https://github.com/initcron/CI-Vertx.git
```
This repo consists of one docker-compose file.
```
version: "3"

services:
  app:
    image: <docker-ub-id>/<repo>:latest
    ports:
      - 7000:8080
```
![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/3669fbf1-39b0-4cae-91d0-b219c4998855)

Edit this file. Replace /:latest with your own values.

For me it looks like this. (Note: This is my image name. Do not use this)

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/5023e63b-6725-4fe9-be10-45fe48cd6883)

## Create a Deploy Job

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/a89a8538-036c-4d43-ad50-09cb6ed266e8)

Create a freestyle job called Deploy.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/b0a2ea3b-45d2-4346-b115-e580075644d0)

In Source Code Management step, add the following git repository.
```
https://github.com/initcron/CI-Vertx.git
```
This repository has a docker-compose file.

In Build Trigger, add Docker-Image as a trigger.

![image](https://github.com/haneefmohamed/DevOps-Projects/assets/159698808/cc190a2e-9714-472e-9d67-ff136469ca07)

In Build step, add Execute Shell as a build step and put the following content.
```
~/docker-compose up -d
```
Finally click on save.
