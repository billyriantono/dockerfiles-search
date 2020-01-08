FROM jenkins/jenkins:lts

LABEL MAINTAINER="Stephen Steiner <ssteiner@juniper.net>"

ENV DEBIAN_FRONTEND noninteractive
ENV JAVA_OPTS='-Djenkins.install.runSetupWizard=false -Dhudson.model.DirectoryBrowserSupport.CSP=allow-same-origin -Djavax.net.ssl.trustStore=$JENKINS_HOME/.keystore/cacerts -Djavax.net.ssl.trustStorePassword=changeit'
ENV JENKINS_USER admin
ENV JENKINS_PASS admin
ENV CUSTOM_KEYSTORE=$JENKINS_HOME/.keystore/

USER root

WORKDIR /var/tmp

COPY requirements.txt /var/tmp/requirements.txt
COPY install-plugins.sh /usr/local/bin/install-plugins.sh
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
COPY basic-security.groovy /var/jenkins_home/init.groovy.d/

RUN apt-get update -qq && \
    apt-get install -yqq apt-utils git-core maven openjdk-8-jdk curl libssl-dev build-essential libssl-dev libffi-dev python3-dev \
        sshpass && \
    apt-get clean && \
    apt-get autoremove -y  && \
    rm -rf /var/cache/apt/*

RUN ( curl https://bootstrap.pypa.io/get-pip.py | python3 ) && \
    ( curl -fsSL get.docker.com | bash ) && \
    pip3 install -r requirements.txt && \
    rm -rf /var/tmp/requirements.txt && \
    usermod -aG docker jenkins
RUN chmod +x /usr/local/bin/install-plugins.sh
RUN xargs /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt
RUN touch /var/run/docker.sock && chmod 777 /var/run/docker.sock

USER jenkins

RUN mkdir -p $CUSTOM_KEYSTORE && \
    cp $JAVA_HOME/jre/lib/security/cacerts $CUSTOM_KEYSTORE

VOLUME $CUSTOM_KEYSTORE/cacerts
VOLUME /usr/share/jenkins/ref/plugins
VOLUME /var/jenkins_home

WORKDIR $JENKINS_HOME

HEALTHCHECK --interval=1m --timeout=3s CMD curl -s -w "%{http_code}" http://localhost:8080 -o /dev/null || exit 1
