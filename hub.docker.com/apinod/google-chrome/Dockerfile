FROM node:latest
MAINTAINER angelmpino87@yahoo.com

ENV CHROME_PACKAGE="google-chrome-stable_current_amd64.deb"

COPY ${CHROME_PACKAGE} ./

WORKDIR /

RUN dpkg --unpack ${CHROME_PACKAGE} && \
    apt-get update && apt-get install -f -y

