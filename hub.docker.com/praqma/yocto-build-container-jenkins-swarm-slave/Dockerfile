# Base image for building Yocto images
FROM praqma/yocto-build-container:ubuntu16.04-0.0.1

ENV JENKINS_SWARM_VERSION 2.2
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk

# We need to install java so we can run swarm slave
USER root
RUN apt-get -qq --yes update && \
    apt-get -qq --yes install openjdk-8-jre curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Get Jenkins swarm client
RUN curl --create-dirs -sSLo /var/build/swarm-client-$JENKINS_SWARM_VERSION-jar-with-dependencies.jar http://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/$JENKINS_SWARM_VERSION/swarm-client-$JENKINS_SWARM_VERSION-jar-with-dependencies.jar && chmod 755 /var/build

COPY start.sh /var/build/start.sh
RUN chmod 755 /var/build/start.sh
RUN chown -R builduser /var/build

USER builduser

ENTRYPOINT ["/usr/local/bin/dumb-init", "--", "/var/build/start.sh"]