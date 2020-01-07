############################################################
# Dockerfile to build jenkins swarm slaves container images that can handle java8 with maven
# Based on maven:latest
############################################################

FROM maven:latest

MAINTAINER Holger Zunker <holger50@gmx.de>

# Create a non-root user
RUN useradd -m user
WORKDIR /home/user

RUN env | grep -E "(JENKINS|JAVA)" > /etc/docker.properties

# Install Git and dependencies
USER root
RUN apt-get update && apt-get -y upgrade
 

USER user

#Install Jenkins dependencies
ENV JENKINS_MASTER_USERNAME="jenkins" \
    JENKINS_MASTER_PASSWORD="jenkins" \
    JENKINS_MASTER_URL="http://jenkins:8080/" \
    JENKINS_SLAVE_MODE="exclusive" \
    JENKINS_SLAVE_NAME="swarm-$RANDOM" \
    JENKINS_SLAVE_WORKERS="1" \
    JENKINS_SLAVE_LABELS="" \
    AVD=""
ENV JENKINS_SLAVE_ROOT="/home/user/"
ENV HOME=/home/jenkins-slave \
    JENKINS_SWARM_VERSION=3.8 \
    JENKINS_SWARM_JAR_PATH=/home/user
ENV JENKINS_SWARM_JAR=${JENKINS_SWARM_JAR_PATH}/swarm.jar
COPY scripts/entrypoint.sh /home/user/scripts/

RUN mkdir -p "$JENKINS_SLAVE_ROOT"
# Install Jenkins slave (swarm)
RUN mkdir -p $JENKINS_SWARM_JAR_PATH \
    && chmod 755 $JENKINS_SWARM_JAR_PATH \
    && curl -SLo $JENKINS_SWARM_JAR http://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/$JENKINS_SWARM_VERSION/swarm-client-$JENKINS_SWARM_VERSION.jar

#ADD entrypoint.sh /usr/bin/
USER root
RUN chmod +x /home/user/scripts/entrypoint.sh
RUN chown -R user:user /home/user/scripts/*
ENTRYPOINT /home/user/scripts/entrypoint.sh

USER user
VOLUME ${HOME}
WORKDIR ${HOME}





