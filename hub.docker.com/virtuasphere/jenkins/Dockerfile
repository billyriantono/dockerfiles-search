FROM jenkins

# Declare maintainer
MAINTAINER Woodruff <sansonthomas28@gmail.com>

USER root

ENV DEBIAN_FRONTEND noninteractive

RUN curl -sSL https://get.docker.com/ | sh \
    && rm -rf /var/lib/apt/lists/*

RUN usermod -aG docker jenkins

USER jenkins

COPY plugins.txt /usr/share/jenkins/plugins.txt

RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

WORKDIR /var/jenkins_home

