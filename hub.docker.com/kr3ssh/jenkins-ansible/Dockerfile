FROM jenkins/jenkins:lts

USER root

RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    apt-transport-https

RUN echo 'deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main' >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367

RUN echo 'deb https://download.docker.com/linux/ubuntu xenial stable' >> /etc/apt/sources.list
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    ansible \
    docker-ce

USER jenkins
