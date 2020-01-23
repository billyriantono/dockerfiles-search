ARG JENKINS_VERSION=2.112-slim
FROM jenkins/jenkins:${JENKINS_VERSION}

LABEL authors="Artur Stolear <artur.stolear@gmail.com>"

ARG JENKINS_SERVER_URL=http://localhost:8080
ENV JENKINS_SERVER_URL=${JENKINS_SERVER_URL}

# Install docker
ARG DOCKER_VERSION=17.12.1-ce
USER root
RUN curl -fL -o docker.tgz "https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_VERSION}.tgz" \
    && tar --extract --file docker.tgz --strip-components 1 --directory /usr/local/bin/ \
    && apt-get update && apt-get install -y nano net-tools iputils-ping
USER ${user}

# Set arguments for Jenkins
ARG JAVA_OPTS
ENV JAVA_OPTS "-Djenkins.install.runSetupWizard=false -Djenkins.CLI.disabled=true ${JAVA_OPTS:-}"
ENV JENKINS_REF /usr/share/jenkins/ref

# Install plugins
COPY plugins.txt $JENKINS_REF/plugins.txt
RUN /usr/local/bin/install-plugins.sh < $JENKINS_REF/plugins.txt

# Copy configuration scripts that will be executed by groovy
COPY ./init.groovy.d/*.groovy       $JENKINS_REF/init.groovy.d/
COPY ./init.groovy.mixins/*.groovy  $JENKINS_REF/init.groovy.mixins/
COPY ./props/*.properties           $JENKINS_HOME/