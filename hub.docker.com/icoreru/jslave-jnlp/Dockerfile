FROM docker:18-dind
ARG JSLAVE_VERSION="3.29"
ENV JENKINS_MASTER="http://localhost:8080"
ENV JENKINS_SLAVE_NAME="jslave-dind"
ENV JENKINS_HOME="/opt/jenkins"
RUN echo "===> Installing software..." && \
    apk --update add curl git bash openjdk8 jq tini ca-certificates nss && \
    \
    echo "===> Installing JSlave..." && \
    curl --create-dirs -sSLo /usr/share/jenkins/slave.jar http://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/$JSLAVE_VERSION/remoting-$JSLAVE_VERSION.jar && \
    chmod 755 /usr/share/jenkins && \
    chmod 644 /usr/share/jenkins/slave.jar && \
    \
    echo "===> Cleaning..." && \
    rm -rf /var/cache/apk/* && \
    rm -rf /tmp/*
COPY ./run.sh /usr/local/bin/
WORKDIR $JENKINS_HOME
ENTRYPOINT ["/sbin/tini", "--"]
CMD ["/usr/local/bin/run.sh"]
