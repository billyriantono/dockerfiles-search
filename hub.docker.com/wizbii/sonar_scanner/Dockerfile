FROM openjdk:10-slim

ARG NODEJS_VERSION=10
ARG SONAR_SCANNER_VERSION="4.0.0.1744"
ARG TYPESCRIPT_VERSION="3.2.4"

ENV SONAR_SCANNER_NAME "sonar-scanner-cli-$SONAR_SCANNER_VERSION"
ENV SONAR_SCANNER_FOLDER_NAME "sonar-scanner-$SONAR_SCANNER_VERSION"

WORKDIR /sonar-scanner

RUN apt-get update && apt-get install -y curl gnupg && \
    curl -sL https://deb.nodesource.com/setup_$NODEJS_VERSION.x | bash - && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && \
    apt-get install -y unzip wget nodejs yarn && \
    wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-$SONAR_SCANNER_VERSION.zip && \
    unzip $SONAR_SCANNER_NAME.zip && \
    yarn global add typescript@$TYPESCRIPT_VERSION

ENV NODE_PATH "/usr/local/share/.config/yarn/global/node_modules/"
ENV PATH $PATH:/sonar-scanner/$SONAR_SCANNER_FOLDER_NAME/bin
