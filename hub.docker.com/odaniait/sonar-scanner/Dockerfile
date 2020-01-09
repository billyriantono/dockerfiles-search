FROM ubuntu:latest

ENV SONAR_VERSION="3.3.0.1492"

WORKDIR /opt

RUN apt-get update && apt-get install -y curl unzip && rm -rf /var/lib/apt/lists/*
RUN curl -o ./sonarscanner.zip -L https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_VERSION}-linux.zip && \
	unzip sonarscanner.zip && \
	rm sonarscanner.zip && \
	mv sonar-scanner-${SONAR_VERSION}-linux sonar-scanner
RUN groupadd app && useradd -g app -r --shell /bin/bash --create-home app

ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/sonar-scanner/bin

WORKDIR /home/app
USER app

