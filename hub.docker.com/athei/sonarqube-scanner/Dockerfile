FROM alpine:latest
## Based on this example http://stackoverflow.com/a/40612088/865222
ENV SONAR_SCANNER_VERSION 3.0.3.778

RUN apk add --no-cache openjdk8-jre && apk add --no-cache openssl && apk add --no-cache ca-certificates && \
    wget https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_SCANNER_VERSION}.zip && \
    unzip sonar-scanner-cli-${SONAR_SCANNER_VERSION} && \
    ln -s /sonar-scanner-${SONAR_SCANNER_VERSION}/bin/sonar-scanner /usr/bin/sonar-scanner && \
    apk del ca-certificates && apk del openssl

RUN apk add --no-cache git
