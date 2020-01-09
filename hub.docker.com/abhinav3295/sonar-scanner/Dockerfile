FROM openjdk:8-alpine

LABEL maintainer="Abhinav Suryavanshi <abhinav3295@gmail.com>"

ENV TZ=Asia/Singapore
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

WORKDIR /root

RUN apk update && \
    apk add --no-cache curl python3 && \
    apk add --no-cache --virtual .build-deps git python3-dev libc-dev gcc && \
    pip3 install --upgrade pip pylint setuptools && \
    apk del .build-deps

ARG SCANNER_VER=3.3.0.1492

ENV DOWNLOAD_URL="https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SCANNER_VER}.zip"

RUN env && \
        curl --insecure -OL ${DOWNLOAD_URL} && \
        mkdir sonar_scanner && \
        unzip -d sonar_scanner sonar-scanner-cli-${SCANNER_VER}.zip && \
        mv sonar_scanner/* sonar_home && \
        rm -rf sonar_scanner $SCANNER_VER.zip

ENV SONAR_RUNNER_HOME=/root/sonar_home
ENV PATH ${SONAR_RUNNER_HOME}/bin:$PATH

CMD sonar-scanner -Dsonar.projectBaseDir=./src
