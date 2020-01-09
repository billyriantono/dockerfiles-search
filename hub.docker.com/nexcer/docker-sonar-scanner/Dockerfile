FROM openjdk:11-jre-slim

ENV SONAR_RUNNER_VERSION=3.2.0.1227 \
  NODE_VERSION=8.9.4

# Installation Basics
RUN apt-get update &&  \
  apt-get install -y git wget curl unzip bzip2 libfontconfig build-essential python python-dev

# Install NodeJS
RUN curl --retry 3 -SLO "http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" && \
  tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 && \
  rm "node-v$NODE_VERSION-linux-x64.tar.gz"

RUN curl -o ./sonar-scanner.zip --silent --location https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-$SONAR_RUNNER_VERSION.zip \
    && unzip sonar-scanner.zip \
    && mv sonar-scanner-$SONAR_RUNNER_VERSION /etc/sonar-scanner \
    && rm sonar-scanner.zip

ENV SONAR_RUNNER_HOME=/etc/sonar-scanner
ENV PATH $PATH:/etc/sonar-scanner/bin
