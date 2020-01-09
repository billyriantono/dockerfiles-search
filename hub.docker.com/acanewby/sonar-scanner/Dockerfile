FROM acanewby/jdk:8-ubuntu

LABEL maintainer="acanewby@yahoo.com"
LABEL description="Provides SonarQube scanner CLI on Ubuntu"

# Update OS package repo and install basic required packages
RUN apt-get update && \
    apt-get install -y unzip nodejs

# General environment setup
ARG SCRATCH=/scratch

# ------------------------------------------------------

WORKDIR /opt/sonar-scanner/

ARG CLI_BUILD=3.3.0.1492
ARG CLI_VER=3.3.0

ARG CLI_ARCHIVE=${SCRATCH}/scanner-${CLI_VER}.tar.gz

RUN mkdir -p ${SCRATCH} && \
    curl -L https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${CLI_BUILD}.zip -o ${CLI_ARCHIVE} && \
    unzip ${CLI_ARCHIVE} && \
    ln -s ./sonar-scanner-${CLI_BUILD} ${CLI_VER} && \
    rm -f ${CLI_ARCHIVE}

ENV SONAR_RUNNER_HOME /opt/sonar-scanner/$CLI_VER
ENV PATH ${SONAR_RUNNER_HOME}/bin:$PATH

# ------------------------------------------------------

# Standard start conditions
WORKDIR /home
CMD ["/bin/bash"]