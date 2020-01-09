FROM jenkins/ssh-slave
RUN apt-get update && \
    apt-get -qy full-upgrade && \
    apt-get install -qy git && \
    apt-get install -qy openjdk-8-jdk;
