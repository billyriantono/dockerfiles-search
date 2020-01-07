FROM node:8.12.0

RUN apt-get update \
  && apt-get install -y --no-install-recommends graphicsmagick \
  && apt-get autoremove -y \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
