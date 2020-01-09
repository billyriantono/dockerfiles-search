FROM jenkins/jenkins:lts-alpine

ENV JENKINS_UC_DOWNLOAD=http://ftp-nyc.osuosl.org/pub/jenkins
ENV CURL_OPTIONS -sSfLk --ipv4 

# Plugins

COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/plugins.txt

# Config

## Credentials

COPY config/credentials.xml /usr/share/jenkins/ref/credentials.xml

## Nodes

COPY nodes/mac/config.xml /usr/share/jenkins/ref/nodes/mac/config.xml 

# Use preinstalled plugins

RUN echo 2.0 > /usr/share/jenkins/ref/jenkins.install.UpgradeWizard.state