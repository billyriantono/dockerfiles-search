
FROM node:alpine
LABEL maintainer "Ryan Desfosses <ryan@desfo.org>"

# git required by resume-cli
# fontconfig required by hackmyresume
RUN apk --update add git fontconfig\
    && rm -rf /var/cache/apk/*

ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD 1
RUN npm install -g resume-cli hackmyresume

WORKDIR /home/node/app
