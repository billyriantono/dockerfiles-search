FROM alpine:3.6

LABEL MAINTAINER="Aurelien PERRIER <a.perrier89@gmail.com>"
LABEL APP="jenkins"
LABEL APP_VERSION="2.60.2"
LABEL APP_DESCRIPTION="build"

ENV TIMEZONE Europe/Paris
ENV JENKINS_VERSION 2.93
ENV GOSU_VERSION 1.10
ENV TINI_VERSION 0.14.0

ENV JENKINS_HOME /var/jenkins_home
ENV CATALINA_OPTS ${CATALINA_OPTS} -Djava.awt.headless=true
ENV CATALINA_OPTS ${CATALINA_OPTS} -Xmx512m
ENV CATALINA_OPTS ${CATALINA_OPTS} -XX:MaxPermSize=128m
ENV COPY_REFERENCE_FILE_LOG ${JENKINS_HOME}/copy_reference_file.log

RUN apk add --no-cache --virtual .build-deps wget tar
RUN apk add --no-cache openjdk8-jre bash ttf-dejavu openssh-client curl unzip coreutils

RUN mkdir -p /usr/share/jenkins/ /usr/share/jenkins/ref/
RUN wget --no-check-certificate -q -O /usr/share/jenkins/jenkins.war https://repo.jenkins-ci.org/public/org/jenkins-ci/main/jenkins-war/${JENKINS_VERSION}/jenkins-war-${JENKINS_VERSION}.war
RUN wget --no-check-certificate -q -O /usr/bin/tini https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini-static-amd64

RUN chmod +x /usr/bin/tini

WORKDIR ${JENKINS_HOME}

RUN addgroup jenkins && \
        adduser -s /bin/false -G jenkins -S -D jenkins && \
        apk del .build-deps

COPY ./scripts/start.sh /usr/local/bin/jenkins.sh

VOLUME [ "${JENKINS_HOME}" ]

EXPOSE 8080

ENTRYPOINT ["/usr/bin/tini", "--", "/usr/local/bin/jenkins.sh"]