FROM openjdk:11-jdk-slim

RUN apt-get update && apt-get install -y python-pip && \
  pip install awscli

RUN apt install -y apt-transport-https ca-certificates curl software-properties-common && \
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
 add-apt-repository -y "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" && \
 apt update && \
 apt install -y docker-ce

 
