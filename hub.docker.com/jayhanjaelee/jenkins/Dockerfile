FROM jenkins/jenkins:lts
MAINTAINER Jay Lee <jay@hanjaelee.com>

USER root

RUN apt-get update && \
	apt-get upgrade -y -q && \
	apt-get install -y -q sudo curl apt-transport-https ca-certificates gnupg2 software-properties-common && \
	echo "jenkins ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
	curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
	add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
	apt-get update && \
	apt-get install -y -q docker-ce

RUN usermod -aG docker jenkins

USER jenkins
