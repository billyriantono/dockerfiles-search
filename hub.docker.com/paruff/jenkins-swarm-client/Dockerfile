FROM openjdk:8-jdk-alpine

ENV JENKINS_SWARM_VERSION 3.13

RUN apk add --no-cache wget docker openssh-client && \
	mkdir -p /jenkins/wks && \
	chmod -R 777 /jenkins && \
	wget https://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/$JENKINS_SWARM_VERSION/swarm-client-$JENKINS_SWARM_VERSION.jar -O /jenkins/swarm-client.jar

ENTRYPOINT [ "java", "-jar", "/jenkins/swarm-client.jar", "-fsroot", "/jenkins/wks" ]
CMD [ "-help" ]
