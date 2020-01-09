FROM node:lts-jessie
LABEL maintainer="dave@salte.io"

RUN apt-get update && \
    apt-get install -y zip

RUN wget -P /opt https://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/5.2.4/flyway-commandline-5.2.4-linux-x64.tar.gz && \
    cd /opt && \
    tar -xvf flyway-commandline-5.2.4-linux-x64.tar.gz && \
    rm flyway-commandline-5.2.4-linux-x64.tar.gz

RUN wget -P /opt https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.3.0.1492-linux.zip && \
    cd /opt && \
    unzip sonar-scanner-cli-3.3.0.1492-linux.zip && \
    rm sonar-scanner-cli-3.3.0.1492-linux.zip

ENV PATH $PATH:/opt/flyway-5.2.4:/opt/sonar-scanner-3.3.0.1492-linux/bin
ENV SONAR_RUNNER_HOME /opt/sonar-scanner-3.3.0.1492-linux
