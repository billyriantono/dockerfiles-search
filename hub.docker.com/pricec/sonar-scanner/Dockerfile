ARG DEBIAN_VERSION=buster-20190610

FROM debian:${DEBIAN_VERSION} as builder
ARG SONAR_VERSION=4.2.0.1873

RUN apt-get update && apt-get install -y wget unzip && \
    wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_VERSION}-linux.zip && \
    unzip sonar-scanner-cli-${SONAR_VERSION}-linux.zip && \
    mv sonar-scanner-${SONAR_VERSION}-linux /sonar

FROM debian:${DEBIAN_VERSION}

COPY --from=builder /sonar /sonar
WORKDIR /sonar
ENTRYPOINT ["bin/sonar-scanner"]
CMD []
