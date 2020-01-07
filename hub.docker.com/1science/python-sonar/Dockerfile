FROM python:3.6-slim

ENV SONAR_SCANNER_VERSION="3.2.0.1227"

WORKDIR /root

RUN apt-get update
RUN apt-get install -y wget unzip
RUN wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip
RUN unzip sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip
RUN rm sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip
RUN ln -s sonar-scanner-${SONAR_SCANNER_VERSION}-linux/ sonar-scanner

RUN apt-get purge -y --auto-remove unzip \
    && rm -rf /var/lib/apt/lists/*

ENV PATH="/root/sonar-scanner/bin:${PATH}"

RUN mkdir /app
WORKDIR /app
