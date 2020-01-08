FROM ubuntu

MAINTAINER Darryl Bresland <darryl.bresland@seopa.com>

RUN apt-get -y update
RUN apt-get install -y openjdk-7-jre wget unzip
RUN adduser --quiet jenkins
RUN echo "jenkins:jenkins" | chpasswd
RUN wget -O /home/jenkins/swarm-client-2.0-jar-with-dependencies.jar http://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/2.0/swarm-client-2.0-jar-with-dependencies.jar
ADD startup.sh /usr/bin/startup.sh
RUN chmod +x /usr/bin/startup.sh
USER jenkins
ENTRYPOINT ["/usr/bin/startup.sh"]