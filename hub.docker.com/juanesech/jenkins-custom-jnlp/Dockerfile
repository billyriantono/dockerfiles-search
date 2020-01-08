FROM jenkins/jnlp-slave:latest

USER root
RUN apt-get update
RUN apt-get install -y python-pip maven
RUN pip install awscli

USER jenkins
