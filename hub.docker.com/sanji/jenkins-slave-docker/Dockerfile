FROM sanji/jenkins-swarm-slave:1.22-jdk8

MAINTAINER Zack YL Shih <zackyl.shih@moxa.com>

USER root

RUN apt-get update && \
    apt-get install -y sudo git-core && \
    rm -rf /var/lib/apt/lists/* # 20150323

RUN groupadd docker -g 995 \
	&& adduser jenkins-slave docker \
	&& adduser jenkins-slave sudo

RUN echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER jenkins-slave
