FROM jenkins:latest

USER root
RUN apt-get update
RUN apt-get install -y apt-transport-https ca-certificates curl sudo
RUN curl -sSL https://get.docker.com/ | sh

RUN curl -L https://github.com/docker/compose/releases/download/1.20.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

USER jenkins
