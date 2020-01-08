# Base image for building AOSP
FROM praqma/aosp-build-container:0.1.1

# Add support for proxies.
# Values should be passed as build args
# http://docs.docker.com/engine/reference/builder/#arg
ENV http_proxy ${http_proxy:-}
ENV https_proxy ${https_proxy:-}
ENV no_proxy ${no_proxy:-}
ARG JAVA_OPTS
ENV JAVA_OPTS ${JAVA_OPTS:-}

# We are not using the latest version (2.2 at the moment of writing)
# because there seems to be issue introdiced starting from 2.1
# that makes swarm client ignore no_proxy settings so it tries to connect to master
# through the proxy which results in error described here
# https://groups.google.com/forum/#!topic/jenkinsci-users/bdZP3Gpj7x4
ENV JENKINS_SWARM_VERSION 2.0
ENV JAVA_HOME /usr/lib/jvm/java-1.7-openjdk

# Get Jenkins swarm client
RUN curl --create-dirs -sSLo /var/build/swarm-client-$JENKINS_SWARM_VERSION-jar-with-dependencies.jar http://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/$JENKINS_SWARM_VERSION/swarm-client-$JENKINS_SWARM_VERSION-jar-with-dependencies.jar

COPY start.sh /var/build/start.sh

ENTRYPOINT ["/usr/local/bin/dumb-init", "--", "/var/build/start.sh"]