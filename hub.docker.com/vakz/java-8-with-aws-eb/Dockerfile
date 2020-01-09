FROM openjdk:8

RUN apt-get update -qq \
    && apt-get install -y -qq python-pip \
    && pip install awsebcli \
    && apt-get clean