# Set the base image to Ubuntu
FROM ubuntu:14.04

# File Author / Maintainer
MAINTAINER @P3Geek

# Add the application resources URL
# RUN echo "deb http://archive.ubuntu.com/ubuntu/ $(lsb_release -sc) main universe" >> /etc/apt/sources.list

# Update the soruces list and install basic applications
RUN apt-get update && apt-get install -y \
        tar git curl nano wget dialog net-tools build-essential python python-dev python-distribute python-pip

ADD . /twitter-consumer

# Get pip to download and install requirements:
RUN pip install -r /twitter-consumer/requirements.txt

#RabbitMQ Task Queue
ENV TASK_QUEUE rabbitmq
ENV RABBITMQ_URI rabbitmq.default.svc.cluster.local

# The web ports for Cloud Foundry
ENV PORT 8080

# Expose ports (same as PORT)
EXPOSE 8080

# Set the default directory where CMD will execute
WORKDIR /twitter-consumer

# Set the default command to execute
# when creating a new container
CMD python -u twitter-consumer.py
