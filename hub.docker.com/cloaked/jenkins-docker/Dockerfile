FROM jenkins/jenkins

LABEL maintainer "dockerhub@cloaked.ch"

USER root

# add nodejs repo 
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -

# install deps
RUN apt-get update && apt-get install -y \
    bsdmainutils \
    nodejs \
 && rm -rf /var/lib/apt/lists/*

# install docker cli
RUN mkdir -p /tmp/_install && cd /tmp/_install && wget https://download.docker.com/linux/static/stable/x86_64/docker-18.09.5.tgz  && tar -xvzf docker-18.09.5.tgz  && cd docker && cp docker /usr/bin/docker && rm -rf  /tmp/_install
RUN chmod +x /usr/bin/docker

# add jenkins to docker group 
RUN groupadd -g 999 docker
RUN usermod -a -G docker jenkins

# install docker-compose 
RUN curl -L https://github.com/docker/compose/releases/download/1.24.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

# show env 
RUN env

USER jenkins
