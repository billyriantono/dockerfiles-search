FROM csanchez/jenkins-swarm-slave

MAINTAINER luizhmc@gmail.com

USER root

RUN apt-get update
RUN apt-get install -y ansible sshpass && rm -rf /var/lib/apt/lists/*

USER jenkins-slave
