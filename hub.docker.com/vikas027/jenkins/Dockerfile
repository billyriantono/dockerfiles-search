# https://hub.docker.com/_/jenkins/
FROM java:8-jdk

# Suppress apt installation warnings
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
	apt-get -y install git curl zip lsof graphviz

ENV JENKINS_HOME=/var/jenkins_home \
    JENKINS_SLAVE_AGENT_PORT=50000

# Initialize default variable of arguments
ARG user=jenkins
ARG group=jenkins
ARG uid=2000
ARG gid=2000

RUN echo ${gid} ${group}

# Jenkins is run with user `jenkins`, uid = 1000
# If you bind mount a volume from the host or a data container, 
# ensure you use the same uid
RUN groupadd -g ${gid} ${group} && \
    useradd -d ${JENKINS_HOME} -u ${uid} -g ${gid} -m -s /bin/bash ${user}

# Jenkins home directory is a volume, so configuration and build history can be persisted and survive image upgrades
VOLUME /var/jenkins_home

# `/usr/share/jenkins/ref/` contains all reference configuration we want 
# to set on a fresh new installation. Use it to bundle additional plugins 
# or config file with your custom jenkins Docker image.
RUN mkdir -p /usr/share/jenkins/ref/init.groovy.d

COPY init.groovy /usr/share/jenkins/ref/init.groovy.d/tcp-slave-agent-port.groovy

# jenkins version being bundled in this docker image
ARG JENKINS_VERSION=2.26

# Can be used to customize where jenkins.war get downloaded from
ARG JENKINS_URL=http://repo.jenkins-ci.org/public/org/jenkins-ci/main/jenkins-war/${JENKINS_VERSION}/jenkins-war-${JENKINS_VERSION}.war

# could use ADD but this one does not check Last-Modified header neither does it allow to control checksum 
# see https://github.com/docker/docker/issues/8331
RUN curl -fsSL ${JENKINS_URL} -o /usr/share/jenkins/jenkins.war

ENV JENKINS_UC https://updates.jenkins.io
ENV JENKINS_UC_DOWNLOAD=${JENKINS_UC}/download
RUN chown -R ${user} ${JENKINS_HOME} /usr/share/jenkins/ref

# 8080  for main web interface
# 50000 will be used by attached slave agents
EXPOSE 8080 50000

ENV COPY_REFERENCE_FILE_LOG $JENKINS_HOME/copy_reference_file.log

USER ${user}

COPY jenkins-support /usr/local/bin/jenkins-support
COPY jenkins.sh /usr/local/bin/jenkins.sh

# Install Jenkins plugins
# COPY plugins.sh /usr/local/bin/plugins.sh  (plugins.sh is not recommended now)
# RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

# Use this to install Plugins
COPY plugins.txt /usr/share/jenkins/plugins.txt
COPY install-plugins.sh /usr/local/bin/install-plugins.sh
RUN /usr/local/bin/install-plugins.sh `cat /usr/share/jenkins/plugins.txt | tr '\n' ' '`

# Clean Up
USER root

# Install Ansible
ARG ANSIBLE_VERSION=2.1.2.0
RUN apt-get -y install git gcc python-dev python-pip sshpass libffi-dev libssl-dev && \
    pip install --upgrade pip && \
    pip install --upgrade ansible==${ANSIBLE_VERSION} paramiko PyYAML Jinja2 httplib2 six cffi pexpect setuptools 

# yaml2json
#RUN apt-get -y install npm && npm install yaml-to-json -g

# For Managing Windows
#RUN pip install "pywinrm>=0.1.1"
#RUN apt-get -y install python-dev libkrb5-dev
#RUN pip install kerberos

# Setup basic ansible
RUN mkdir -p /etc/ansible/facts.d /etc/ansible/roles /etc/ansible/playbooks


# Clean Up
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/*

CMD ["/usr/local/bin/jenkins.sh"]
