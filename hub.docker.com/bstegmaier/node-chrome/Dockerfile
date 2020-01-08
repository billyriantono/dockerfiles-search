FROM node:8

RUN apt-get update && apt-get install -y chromium

COPY chrome-wrapper /usr/bin/chrome-wrapper
RUN ln -s /usr/bin/chrome-wrapper /usr/bin/google-chrome && ln -s /usr/bin/chrome-wrapper /usr/bin/chromium-browser
