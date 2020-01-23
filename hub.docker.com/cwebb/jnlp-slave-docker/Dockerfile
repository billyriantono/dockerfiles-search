FROM jenkins/jnlp-slave:3.19-1

MAINTAINER Christopher Webb <cwebb@thoughtworks.com>

USER root

RUN apt-get update                                                          && \
    apt-get -y install apt-transport-https ca-certificates && \
	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
	echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable" \
        > /etc/apt/sources.list.d/docker.list    && \
	apt-get update && \
	apt-get -y install docker-ce
	
RUN usermod -a -G docker jenkins

USER jenkins
