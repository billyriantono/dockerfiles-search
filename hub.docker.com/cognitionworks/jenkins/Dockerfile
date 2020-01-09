### base image
FROM jenkins/jenkins:lts


### installing additional packages
USER root
RUN apt-get update && apt-get install -y ruby


### switching back to jenkins user
USER jenkins
