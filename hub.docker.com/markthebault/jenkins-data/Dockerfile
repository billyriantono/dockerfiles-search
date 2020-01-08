FROM alpine:3.4

ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000

ARG JENKINS_HOME="/var/jenkins_home"
ARG JENKINS_LOGS="/var/log/jenkins"

ENV JENKINS_HOME /var/jenkins_home


RUN addgroup -g ${gid} ${group} \
    && adduser -h ${JENKINS_HOME} -u ${uid} -G ${group} -s /bin/bash -D ${user}


VOLUME ${JENKINS_HOME}

RUN mkdir -p /var/log/jenkins
#RUN chown -R ${group}:${user} ${JENKINS_LOGS}

VOLUME ${JENKINS_LOGS}


USER ${user}
CMD ["echo", "Data container for Jenkins"]
