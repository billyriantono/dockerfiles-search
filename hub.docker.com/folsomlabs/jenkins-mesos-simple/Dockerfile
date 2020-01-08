FROM folsomlabs/mesos
MAINTAINER Benjamin Staffin "ben@folsomlabs.com"

RUN apt-get update
RUN apt-get install -qfy openjdk-7-jre-headless git
ADD http://mirrors.jenkins-ci.org/war-stable/1.609.1/jenkins.war /opt/jenkins.war
RUN chmod 644 /opt/jenkins.war

RUN addgroup --gid 1001 jenkins
RUN adduser --system --ingroup jenkins --home /var/lib/jenkins --shell /bin/bash --uid 1001 jenkins
RUN adduser jenkins sudo
ADD docker-entrypoint.sh /docker-entrypoint.sh

ENV JENKINS_HOME /var/lib/jenkins
VOLUME /var/lib/jenkins

USER jenkins
ENTRYPOINT ["/docker-entrypoint.sh"]
EXPOSE 8080
CMD [""]

# You can set JVM_ARGS at runtime to pass arguments to java
# Any commandline args will go to jenkins.
