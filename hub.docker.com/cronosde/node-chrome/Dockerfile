FROM node:lts

RUN apt-get update \
  && wget --quiet https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
  && apt-get install -y -qq ./google-chrome-stable_current_amd64.deb