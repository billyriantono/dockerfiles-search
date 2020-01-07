FROM tcloud/ubuntu-android-base
MAINTAINER tcloud

USER root

ENV JENKINS_VERSION="1.656" \
    JENKINS_HOME="/opt/jenkins/home"

# Install Jenkins
ADD http://mirrors.jenkins-ci.org/war/${JENKINS_VERSION}/jenkins.war /opt/jenkins/bin/jenkins.war
ADD files/jenkins/run /etc/service/jenkins/run

RUN mkdir -p ${JENKINS_HOME} && \
	chmod 644 /opt/jenkins/bin/jenkins.war && \
	chmod +x /etc/service/jenkins/run && \
	rm -rf /etc/service/sshd /etc/service/syslog-forwarder /etc/service/syslog-ng

EXPOSE 8080

WORKDIR /data

VOLUME ["/data","/log"]

CMD ["/sbin/my_init"]

# Clean up
RUN apt-get clean && \
	apt-get autoremove -y && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*