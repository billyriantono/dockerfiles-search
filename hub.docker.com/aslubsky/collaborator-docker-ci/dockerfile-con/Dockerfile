FROM openjdk:8-alpine

RUN wget http://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.0.3.778.zip && \
    unzip sonar-scanner-cli-3.0.3.778.zip && \
    rm -rf sonar-scanner-cli-3.0.3.778.zip

RUN mkdir -p /app
WORKDIR /app

ENTRYPOINT '/sonar-scanner-3.0.3.778/bin/sonar-scanner'
