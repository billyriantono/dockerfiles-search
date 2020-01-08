############################################################
# Dockerfile to build jenkins swarm slaves container images that can build and publish new docker images
# Based on debian
############################################################

FROM debian:latest

MAINTAINER Holger Zunker <holger50@gmx.de>

# Create a non-root user
RUN useradd -m user
WORKDIR /home/user

#Install docker 
USER root 

RUN apt-get -qq update && apt-get -qq install -y \
    curl \
    apt-utils \
    apt-transport-https \
    ca-certificates \ 
    ca-certificates-java \
    gnupg2 \
    software-properties-common \
    openjdk-8-jdk \
    ant \
    && apt-get -y upgrade \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && update-ca-certificates -f
    
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME

RUN curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable"
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -

RUN apt-get -qq update && apt-get -qq install -y \
    docker-ce \
    && apt-get -y upgrade \
    && rm -rf /var/lib/apt/lists/*
    
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

#ADD entrypoint.sh /usr/bin/
USER root
RUN chmod +x /home/user/scripts/entrypoint.sh
#RUN chown -R user:user /home/user/scripts/*
ENTRYPOINT /home/user/scripts/entrypoint.sh
RUN usermod -a -G docker user
RUN chown user:user /home/user/ -R
RUN chmod g+rwx "/home/user/" -R

USER user
VOLUME ${HOME}
WORKDIR ${HOME}