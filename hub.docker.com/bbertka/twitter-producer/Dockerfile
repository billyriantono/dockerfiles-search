# Set the base image to Ubuntu
FROM ubuntu:14.04

# File Author / Maintainer
MAINTAINER @P3Geek

# Add the application resources URL
# RUN echo "deb http://archive.ubuntu.com/ubuntu/ $(lsb_release -sc) main universe" >> /etc/apt/sources.list

# Update the soruces list and install basic applications
RUN apt-get update && apt-get install -y \
        tar git curl nano wget dialog net-tools build-essential python python-dev python-distribute python-pip

ADD . /twitter-producer

# Get pip to download and install requirements:
RUN pip install -r /twitter-producer/requirements.txt

#Environment (Keys are fake and are replaced at runtime)
# Bot keys
ENV APP_KEY  LwInchdbrgzrfxOAerglOt5GieCgqsdsfdYE3UV
ENV APP_SECRET FJDjergerg5G8FergergLQViobcbergergSbBPdKvCwxU93JmOnIprtoeAimVLUXmyiM
ENV OAUTH_TOKEN 292erge771e-kxy3bhFTergergl2Kktyzu8ukzyikPScaesrfbuayqgq7gGW
ENV OAUTH_TOKEN_SECRET JFEaeFGGDeSHg3VQcccdI8Pfj7ghvnj67dh

#RabbitMQ Task Queue
ENV TASK_QUEUE rabbitmq
ENV RABBITMQ_URI rabbitmq.default.svc.cluster.local

# What to look for
ENV TRACK bigdata

# The web ports for Cloud Foundry
ENV PORT 8080

# Expose ports (same as PORT)
EXPOSE 8080

# Set the default directory where CMD will execute
WORKDIR /twitter-producer

# Set the default command to execute
# when creating a new container
CMD python -u twitter-producer.py
