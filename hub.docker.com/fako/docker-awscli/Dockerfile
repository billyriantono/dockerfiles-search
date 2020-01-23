FROM python:3.6.4

MAINTAINER Wouter de Winter

RUN pip install awscli

# Allows parsing of json files for AWS ECS deployment
RUN apt-get update && apt-get install -y gettext jq
