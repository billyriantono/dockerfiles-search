FROM dwolla/jenkins-agent-chef
MAINTAINER Dwolla Dev <dev+jenkins-chef-tools@dwolla.com>

ARG BUILD_DATE
ARG VCS_REF
ARG VCS_URL
ARG VERSION

LABEL \
    maintainer="Dwolla Dev <dev+jenkins-chef-tools@dwolla.com>" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="dwolla/jenkins-agent-chef-nvm Dockerfile" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.vcs-ref="${VCS_REF}" \
    org.label-schema.vcs-url="${VCS_URL}" \
    org.label-schema.version="${VERSION}"

COPY jenkins-agent /usr/local/bin/

USER jenkins

ENV NVM_VERSION=v0.33.11

RUN curl -L https://raw.githubusercontent.com/creationix/nvm/${NVM_VERSION}/install.sh | /bin/bash

ENV NVM_DIR="${JENKINS_HOME}/.nvm"

RUN chmod 755 "${JENKINS_HOME}/.nvm/nvm.sh"
