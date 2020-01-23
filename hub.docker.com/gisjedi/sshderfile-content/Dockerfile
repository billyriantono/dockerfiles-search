# ====================================================================== #
# Android SDK Docker Image
# ====================================================================== #

# Base image
# ---------------------------------------------------------------------- #
FROM giorgiopiatti/android-sdk:latest

# Author
# ---------------------------------------------------------------------- #
LABEL maintainer "contact@giorgiopiatti.ch"


# nodejs version
ENV NODE_VERSION="8.x"

#Install curl
RUN apt-get update -qq > /dev/null && \
    apt-get install -qq --no-install-recommends curl

#Install NPM & Node
RUN  echo "installing nodejs, npm" && \
    curl -sL -k https://deb.nodesource.com/setup_${NODE_VERSION} | bash - && \
    apt-get update && \
    apt-get -y install nodejs --no-install-recommends && \
    apt-get clean > /dev/null && \
    rm -rf /var/lib/apt/lists/ && \
    npm install --quiet -g npm > /dev/null

RUN useradd -ms /bin/bash nativescript

COPY docker-entrypoint.sh /docker-entrypoint.sh

# Install NativeScript
RUN npm install -g nativescript@latest && \
    tns error-reporting disable

VOLUME ["/app","/dist"]

WORKDIR /app

CMD ["/docker-entrypoint.sh"]
