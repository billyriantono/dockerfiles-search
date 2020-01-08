FROM jleight/phusion-java:7
MAINTAINER Jonathon Leight <jonathon.leight@jleight.com>

RUN set -x \
  && apt-get update \
  && apt-get install -y wget curl git zip \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
    /tmp/* \
    /var/tmp/*

ENV APP_HOME    /opt/jenkins
ENV APP_DATA    /var/opt/jenkins
ENV APP_VERSION 1.580.3
ENV APP_BASEURL http://mirrors.jenkins-ci.org/war-stable/
ENV APP_PKGNAME jenkins.war
ENV APP_URL     ${APP_BASEURL}/${APP_VERSION}/${APP_PKGNAME}

RUN set -x \
  && groupadd -r -g 300 jenkins \
  && useradd -r -d "${APP_DATA}" -u 300 -g jenkins jenkins \
  && mkdir -p "${APP_DATA}" \
  && chown jenkins:jenkins "${APP_DATA}" \
  && mkdir -p "${APP_HOME}" \
  && curl -kL -o "${APP_HOME}/jenkins.war" "${APP_URL}" \
  && chown -R jenkins:jenkins "${APP_HOME}"

ADD jenkins-service.sh /etc/service/jenkins/run

EXPOSE 8080
EXPOSE 50000
VOLUME ["/var/opt/jenkins"]