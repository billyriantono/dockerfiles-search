FROM jupyter/all-spark-notebook

USER root

RUN apt-get update && yes | apt-get install apt-transport-https ca-certificates curl software-properties-common
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic edge" > /etc/apt/sources.list.d/docker.list

RUN apt-get update && yes | apt-get install pkg-config libssl-dev libsasl2-dev libcurl4-openssl-dev docker-ce

ENV GRANT_SUDO=yes
