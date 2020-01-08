FROM jenkins/jenkins:lts

USER root

#Install node & npm
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get update && apt-get install -y nodejs npm jq rsync

#Add sencha sdk
COPY sencha /opt/Sencha/Cmd/6.2.0.103
RUN chmod -R 777 /opt/Sencha

#Install docker
RUN curl -sSL https://get.docker.com/ | sh

#Install helm
COPY helm /opt/helm
RUN chmod -R 777 /opt/helm

#Install kubectl
COPY kubectl /opt/kubectl
RUN chmod -R 777 /opt/kubectl

USER jenkins

ENV PATH="/opt/kubectl:/opt/helm:${PATH}"

