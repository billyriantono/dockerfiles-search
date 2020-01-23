FROM jenkins/jenkins:2.73.1

ENV DOCKER_GROOVY_FILES=src/docker-jenkins/groovy \
    DOCKER_SHELL_FILES=src/docker-jenkins/shell \
    DOCKER_RESOURCE_FILES=src/docker-jenkins/resources \
    JENKINS_VERSION=2.73.1 \
    JENKINS_HOME=/var/jenkins_home \
    JENKINS_REF=/usr/share/jenkins/ref

# install additional tools
USER root
RUN apt-get update \
    && apt-get install -y \
        apt-utils \
        git \
        unzip \
        vim \
        wget \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sSL https://get.docker.com/ | sh \
    && rm -rf /var/lib/apt/lists/* \
    && usermod -aG docker,staff jenkins

# add hpi bundled plugins
COPY $DOCKER_RESOURCE_FILES/plugins/* $JENKINS_REF/plugins/
# add plugins list
COPY $DOCKER_RESOURCE_FILES/plugins.txt $JENKINS_REF/

# add scripts
COPY $DOCKER_SHELL_FILES/* /usr/bin/

# update mod/own
RUN chmod +x \
    /usr/bin/accept-host-keys \
    /usr/bin/create-git-config \
    /usr/bin/create-keys \
    /usr/bin/print-keys \
    && chown jenkins: -R $JENKINS_REF/plugins/

USER jenkins

# pre-install plugins
RUN cat $JENKINS_REF/plugins.txt | xargs /usr/local/bin/install-plugins.sh

# customize jenkins
COPY $DOCKER_GROOVY_FILES/initial-*.groovy $JENKINS_REF/init.groovy.d/
COPY $DOCKER_GROOVY_FILES/seed-job.groovy /tmp/seed-job.groovy

RUN echo $JENKINS_VERSION > $JENKINS_HOME/jenkins.install.UpgradeWizard.state
RUN echo $JENKINS_VERSION > $JENKINS_HOME/jenkins.install.InstallUtil.lastExecVersion
