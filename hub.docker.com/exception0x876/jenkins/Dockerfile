FROM jenkins/jenkins:2.198

USER root

RUN apt-get update && apt-get install -y python python-pip && pip install awscli && apt-get clean

USER ${user}
