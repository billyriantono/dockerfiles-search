###############################################################################
# kubekit/jenkins-worker
###############################################################################
FROM debian:jessie

ADD backports.list /etc/apt/sources.list.d/
ADD docker.list /etc/apt/sources.list.d/

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D  && \
	apt-get update && \
	apt-get install -y openjdk-8-jre-headless docker-engine && \
	rm -rf /var/lib/apt/lists/*

ADD http://maven.jenkins-ci.org/content/repositories/releases/org/jenkins-ci/plugins/swarm-client/2.0/swarm-client-2.0-jar-with-dependencies.jar /swarm-client.jar

ENTRYPOINT [ "java", "-jar", "/swarm-client.jar" ]
