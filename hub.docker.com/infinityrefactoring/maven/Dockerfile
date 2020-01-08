ARG MAVEN_VERSION=3.5.4-jdk-8
FROM maven:$MAVEN_VERSION

LABEL vendor="Infinity Refactoring" \
      git.repository="https://github.com/InfinityRefactoring/docker-maven" \
      authors="Thomás Sousa Silva (ThomasSousa96)"

RUN apt-get update \
      && apt-get install gnupg2 \
      && apt-get install git

ARG MAVEN_SETTINGS_XML="https://raw.githubusercontent.com/InfinityRefactoring/docker-maven/master/config/.m2/settings.xml"
ADD $MAVEN_SETTINGS_XML /root/.m2/

ARG SCRIPT_GIT_CONFIG="https://raw.githubusercontent.com/InfinityRefactoring/docker-maven/master/config/git/set-git-config"
ADD $SCRIPT_GIT_CONFIG /usr/local/bin/

ARG SCRIPT_ADD_SSH_KEY="https://raw.githubusercontent.com/InfinityRefactoring/docker-maven/master/config/ssh/add-ssh-key"
ADD $SCRIPT_ADD_SSH_KEY /usr/local/bin/

ARG SCRIPT_IMPORT_GPG_KEY="https://raw.githubusercontent.com/InfinityRefactoring/docker-maven/master/config/.m2/import-gpg-key"
ADD $SCRIPT_IMPORT_GPG_KEY /usr/local/bin/

ARG SCRIPT_GET_TARGET_BRANCH="https://raw.githubusercontent.com/InfinityRefactoring/docker-maven/master/config/git/get-target-branch"
ADD $SCRIPT_GET_TARGET_BRANCH /usr/local/bin/

ARG SCRIPT_MVN_SONAR="https://raw.githubusercontent.com/InfinityRefactoring/docker-maven/master/config/sonar/mvn-sonar"
ADD $SCRIPT_MVN_SONAR /usr/local/bin/

ARG IVG="https://github.com/InfinityRefactoring/infinity-version-generator/archive/master.zip"
RUN wget "$IVG" -O /tmp/ivg.zip; \
      unzip /tmp/ivg.zip -d /root/InfinityRefactoring; \
      rm /tmp/ivg.zip; \
      mv /root/InfinityRefactoring/infinity-version-generator-master /root/InfinityRefactoring/infinity-version-generator

ENV PATH="/root/InfinityRefactoring/infinity-version-generator:$PATH"

RUN chmod +x \
      /usr/local/bin/set-git-config \
      /usr/local/bin/add-ssh-key \
      /usr/local/bin/import-gpg-key \
      /usr/local/bin/get-target-branch \
      /usr/local/bin/mvn-sonar \
      /root/InfinityRefactoring/infinity-version-generator/ivg
