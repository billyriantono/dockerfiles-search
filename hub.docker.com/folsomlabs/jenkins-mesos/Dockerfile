FROM folsomlabs/mesos
MAINTAINER ben@folsomlabs.com

RUN apt-get install -qfy git zip curl xmlstarlet

RUN mkdir -p /usr/share/jenkins
RUN curl -s -L https://updates.jenkins-ci.org/download/war/1.565.2/jenkins.war > /usr/share/jenkins/jenkins.war

RUN adduser --system --home /var/lib/jenkins --shell /bin/bash jenkins
RUN mkdir -p /var/lib/jenkins/plugins && chown -R jenkins /var/lib/jenkins
ENV JENKINS_HOME /var/lib/jenkins

# web
ENV PORT0 8080
EXPOSE 8080

# ssh
ENV PORT1 2222
EXPOSE 2222

# for slave agents
ENV PORT2 50000
EXPOSE 50000

# Optional JVM arguments
#ENV JVM_ARGS -Xmx1024m

# Environment variables that you want/need to set:
#ENV mesos_master_url zk://zk.example.com:2181/mesos
#ENV jenkins_admin_email you@yourdomain.com
#ENV jenkins_url http://jenkins.yourdomain.com
#ENV jenkins_authorization_strategy

WORKDIR /var/lib/jenkins/plugins
RUN curl -OsL https://updates.jenkins-ci.org/download/plugins/mesos/0.4.0/mesos.hpi
RUN curl -OsL https://updates.jenkins-ci.org/download/plugins/timestamper/1.5.14/timestamper.hpi
RUN curl -OsL https://updates.jenkins-ci.org/download/plugins/git/2.2.5/git.hpi
RUN curl -OsL https://updates.jenkins-ci.org/download/plugins/credentials/1.16.1/credentials.hpi
RUN curl -OsL https://updates.jenkins-ci.org/download/plugins/scm-api/0.2/scm-api.hpi
RUN curl -OsL https://updates.jenkins-ci.org/download/plugins/git-client/1.10.1/git-client.hpi
RUN curl -OsL https://updates.jenkins-ci.org/download/plugins/jobConfigHistory/2.9/jobConfigHistory.hpi
RUN curl -OsL https://updates.jenkins-ci.org/download/plugins/openid/2.1/openid.hpi
RUN curl -OsL https://updates.jenkins-ci.org/download/plugins/openid4java/0.9.8.0/openid4java.hpi

ADD configs /var/lib/jenkins/
ADD init.groovy.d /var/lib/jenkins/init.groovy.d
ADD runjenkins.sh /tmp/

WORKDIR /var/lib/jenkins
RUN chown -R jenkins /var/lib/jenkins

USER jenkins
CMD /tmp/runjenkins.sh
