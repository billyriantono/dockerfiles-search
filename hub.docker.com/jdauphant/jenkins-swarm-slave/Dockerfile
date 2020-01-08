FROM ubuntu:14.04
MAINTAINER Julien Dauphant
ENV install_dir /opt
ENV swarm_version 1.21

RUN apt-get update
RUN apt-get install -y wget openjdk-7-jre-headless
RUN mkdir -p $install_dir
RUN wget http://maven.jenkins-ci.org/content/repositories/releases/org/jenkins-ci/plugins/swarm-client/${swarm_version}/swarm-client-${swarm_version}-jar-with-dependencies.jar -O ${install_dir}/swarm-client.jar

ENTRYPOINT java -jar ${install_dir}/swarm-client.jar
CMD -master http://jenkins:8080
