FROM twdevops/java:8
MAINTAINER ShawnMa <qsma@thoughtworks.com>

ENV JENKINS_HOME /var/lib/jenkins

## Add repository
RUN \
  wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add - && \
  echo "deb http://pkg.jenkins-ci.org/debian binary/" > /etc/apt/sources.list.d/jenkins.list

## Update and Install packages
RUN \
  apt-get update &&\
  apt-get install -y --no-install-recommends jenkins

## Install scripts
ADD entrypoint.sh /entrypoint.sh
RUN chmod a+x     /entrypoint.sh

## Cleanup
RUN \
  apt-get autoclean -y &&\
  apt-get autoremove -y &&\
  rm -rf /tmp/*  &&\
  rm -rf /var/tmp/* &&\
  rm -rf /var/lib/apt/lists/*

USER jenkins

EXPOSE 8080 50000

WORKDIR /var/lib/jenkins

ENTRYPOINT ["/entrypoint.sh"]

VOLUME ["/var/lib/jenkins"]

