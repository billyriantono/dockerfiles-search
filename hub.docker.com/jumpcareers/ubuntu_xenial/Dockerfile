# Use an official Python runtime as a base image
FROM ubuntu:xenial

# Environment variables
ENV ES_PKG_NAME elasticsearch-5.3.0

# Set the conatiner working directory to /app
# WORKDIR /app

# Copy the current directory contents into the container at /app
# ADD . /app

### Installation
## API
RUN apt-get update
RUN apt-get -y install git
RUN apt-get -y install python2.7
RUN apt-get -y install python-setuptools python-dev build-essential
RUN apt-get -y install libffi-dev
RUN apt-get -y install python-pip
RUN apt-get -y install wget
RUN pip install --upgrade pip

# Switch back to root
WORKDIR /

## MongoDB
RUN apt-get -y install mongodb-server

# Create the MongoDB data directory
RUN mkdir -p /opt/mongodb/db

## Elasticsearch

# Required for add-apt-repository
RUN apt-get -y install software-properties-common 
RUN apt-get update

# Install Java 8
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer


ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# Install Elasticsearch.
RUN \
  cd / && \
  wget https://artifacts.elastic.co/downloads/elasticsearch/$ES_PKG_NAME.tar.gz && \
  tar xvzf $ES_PKG_NAME.tar.gz && \
  rm -f $ES_PKG_NAME.tar.gz && \
  mv /$ES_PKG_NAME /opt/elasticsearch

# Create directory for mongo-connector logs
RUN mkdir -p /tmp/mongo-connector/log

# Expose mongo ports.
#   - 27017: process
#   - 28017: http
EXPOSE 27017
EXPOSE 28017

# Expose Elasticsearch port
EXPOSE 9200

