# Test container
#
#   $ docker build -t docker-node-spec .

FROM debian:stable-slim

ENV APP_DIR=/project \
	COVERAGE_DIR=/project/coverage

# Install dependencies
#   1. NodeJS 10, NPM 6.9
#   2. Headless Chrome
#   3. Yarn
RUN apt-get update && \
    apt-get install -yy wget curl gnupg && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get update && apt-get install -y nodejs && \
    npm install npm@6.9 -g && \
    wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list && \
    apt-get update && \
    apt-get install -y google-chrome-stable xvfb && \
    rm -rf /var/lib/apt/lists/* && \
    set -uex && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    set -uex && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    set -uex && \
    apt-get update && \
    apt-get install -yy yarn build-essential && \
    mkdir -v -p ${APP_DIR}