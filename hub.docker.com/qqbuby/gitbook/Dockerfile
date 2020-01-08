FROM node:8-stretch

LABEL maintainer="ROY XU <qqbuby@gmail.com>"

RUN npm install gitbook-cli -g \
    && gitbook fetch 3 \
    && npm cache clean --force \
    && rm -rf /tmp/* \
    && gitbook --version

RUN apt-get update && apt-get install -y --no-install-recommends \
    calibre \
    fonts-cns11643-kai \
    && rm -rf /var/lib/apt/lists/*


