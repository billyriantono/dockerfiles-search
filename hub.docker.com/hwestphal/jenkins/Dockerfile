FROM dockerfile/java:oracle-java8
MAINTAINER Harald Westphal <h.westphal@gmx.de>

RUN \
  DEBIAN_FRONTEND=noninteractive \
  apt-get -q -y update && \
  apt-get -q -y install docker.io wget git curl zip npm maven ant gradle python-dev python-pip && \
  wget -q -O - http://pkg.jenkins-ci.org/debian-stable/jenkins-ci.org.key | sudo apt-key add - && \
  echo deb http://pkg.jenkins-ci.org/debian-stable binary/ >> /etc/apt/sources.list && \
  apt-get -q -y update && \
  apt-get -q -y install jenkins && \
  ln -s /usr/bin/nodejs /usr/bin/node && \
  git config --global url."https://".insteadOf git:// && \
  git config --global http.sslVerify false && \
  pip install ansible

EXPOSE 8080

ENV JENKINS_HOME /data
ENV JENKINS_PREFIX /

CMD exec java -jar /usr/share/jenkins/jenkins.war --prefix=${JENKINS_PREFIX}
