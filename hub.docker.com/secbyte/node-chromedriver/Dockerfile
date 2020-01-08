FROM node:8.13.0-stretch

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    -y chromium-driver && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*

RUN npm install -g --no-save yarn && \
    chmod +x /usr/local/lib/node_modules/yarn/bin/yarn.js && \
    yarn global upgrade yarn