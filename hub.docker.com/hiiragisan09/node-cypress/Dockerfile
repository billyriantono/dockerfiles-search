FROM node:10.16
MAINTAINER Martyn de Vries "https://github.com/Hiiragisan09"

RUN apt-get update \
  && apt-get install -y libgtk2.0-0 libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2 xvfb \
  \
  # Check node and npm versions
  && node -v \
  && npm -v \

WORKDIR /opt/cypress

RUN echo '{}' > package.json && \
    npm install cypress@3.5.0
