FROM node:7.3-slim
MAINTAINER Julie Ng <hello@julie.io>

# Install packages not included in slim
RUN apt-get update && \
    apt-get install --assume-yes sudo apt-transport-https

# Configure Debian Package Repository & install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && \
    apt-get install yarn
