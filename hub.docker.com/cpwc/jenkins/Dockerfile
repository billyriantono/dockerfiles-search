FROM jenkins/jenkins:lts

USER root

# Setting up AWS CLI
RUN apt-get update
RUN apt-get install -y python jq
RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install awscli

USER jenkins
