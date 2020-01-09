############################################################
# Dockerfile to build jenkins swarm slaves container images that can handle python, node, npm
# Based on node:latest
############################################################

FROM node:latest

MAINTAINER Holger Zunker <holger50@gmx.de>

# Create a non-root user
RUN useradd -m user
WORKDIR /home/user
USER root 

# Install essentials
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y curl git htop man unzip vim wget curl zip unzip apt-utils apt-transport-https ca-certificates gnupg2 software-properties-common && \
  rm -rf /var/lib/apt/lists/*

CMD ["bash"]

# Install Python.
RUN apt-get update && apt-get install -y python python-dev python-pip python-virtualenv && rm -rf /var/lib/apt/lists/*

# Install Java.
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee /etc/apt/sources.list.d/webupd8team-java.list
RUN echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list
RUN apt-key adv --keyserver http://keyserver.ubuntu.com:80 --recv-keys EEA14886
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN apt-get update && apt-get install oracle-java8-installer -y

#Install node
RUN curl -sL https://deb.nodesource.com/setup_9.x | bash -
RUN apt-get install -y nodejs
RUN npm install npm@latest -g

USER root
RUN apt-get update && apt-get -y upgrade
 

USER user

#Install Jenkins dependencies
ENV JENKINS_MASTER_USERNAME="jenkins" \
    JENKINS_MASTER_PASSWORD="jenkins" \
    JENKINS_MASTER_URL="http://jenkins:8080/" \
    JENKINS_SLAVE_MODE="exclusive" \
    JENKINS_SLAVE_NAME="swarm-node-$RANDOM" \
    JENKINS_SLAVE_WORKERS="1" \
    JENKINS_SLAVE_LABELS="Node node python java8 oracle-java8" \
    AVD=""
ENV JENKINS_SLAVE_ROOT="/home/user/"
ENV HOME=/home/user \
    JENKINS_SWARM_VERSION=3.9 \
    JENKINS_SWARM_JAR_PATH=/home/user
ENV JENKINS_SWARM_JAR=${JENKINS_SWARM_JAR_PATH}/swarm.jar
COPY scripts/entrypoint.sh /home/user/scripts/

RUN mkdir -p "$JENKINS_SLAVE_ROOT"
# Install Jenkins slave (swarm)
RUN mkdir -p $JENKINS_SWARM_JAR_PATH \
    && chmod 755 $JENKINS_SWARM_JAR_PATH \
    && curl -SLo $JENKINS_SWARM_JAR http://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/$JENKINS_SWARM_VERSION/swarm-client-$JENKINS_SWARM_VERSION.jar

USER root
RUN env | grep -E "(JENKINS|JAVA)" > /etc/docker.properties

#ADD entrypoint.sh /usr/bin/
USER root
RUN chmod +x /home/user/scripts/entrypoint.sh
RUN chown -R user:user /home/user/scripts/*
ENTRYPOINT /home/user/scripts/entrypoint.sh

USER user
VOLUME ${HOME}
WORKDIR ${HOME}

