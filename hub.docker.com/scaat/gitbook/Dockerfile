FROM node:10.15.0-alpine
LABEL maintainer="Scaat Feng <scaat.feng@gmail.com>"
ARG VERSION=3.2.3
LABEL VERSION=$VERSION
RUN npm install -g gitbook-cli &&\
    gitbook fetch ${VERSION} &&\
    npm cache clear --force &&\
    rm -rf /tmp/*
WORKDIR /opt/doc
EXPOSE 4000 35729
CMD gitbook serve   
