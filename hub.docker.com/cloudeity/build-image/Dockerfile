FROM alpine:latest

RUN apk upgrade --update \
  && apk add nodejs openjdk8-jre wget \
  && rm -rf /var/cache/apk/*

# Install Yarn
RUN npm install -g yarn

# Install sonar-scanner
RUN wget https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.0.3.778.zip -O /tmp/sonar-scanner-cli-3.0.3.778.zip \
    && unzip /tmp/sonar-scanner-cli-3.0.3.778.zip -d / \
    && ln -s /sonar-scanner-3.0.3.778/bin/sonar-scanner /usr/bin/sonar-scanner