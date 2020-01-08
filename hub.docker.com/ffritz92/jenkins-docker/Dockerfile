# base image jenkins
FROM jenkins/jenkins:lts

# install curl
USER root
RUN apt-get -qq update \
   && apt-get -qq -y install \
   curl

# install docker
RUN curl -sSL https://get.docker.com/ | sh
#RUN curl -sSL https://get.docker.com/ | DOCKER_VERSION=18.06.1-ce sh
#RUN curl -sSL https://get.docker.com/ | sed 's/docker-ce/docker-ce=18.06.1-ce/' | sh

# define docker group as my host
RUN groupmod -g 998 docker

# add jenkins user to docker group
RUN usermod -a -G staff,docker jenkins

# working user
USER jenkins

