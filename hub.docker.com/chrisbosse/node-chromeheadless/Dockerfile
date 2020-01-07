FROM node:dubnium

# Inspired by https://hackernoon.com/running-karma-tests-with-headless-chrome-inside-docker-ae4aceb06ed3

# Install Google Chrome
# apt warning: https://github.com/zenato/docker-puppeteer/issues/4#issuecomment-460650503
ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=1
RUN ["/bin/bash", "-c", "set -o pipefail && \
    wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub \
    | apt-key add -"]
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN apt-get update && apt-get install -y \
    google-chrome-stable \
 && rm -rf /var/lib/apt/lists/*

