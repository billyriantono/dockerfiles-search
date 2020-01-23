FROM node:8.11
MAINTAINER dlohani48 [at] gmail [dot] com

ENV DEBIAN_FRONTEND=noninteractive \
    ELECTRON_VERSION=2.0.8 \
    # Fix for the issue with Selenium, as described here:
    # https://github.com/SeleniumHQ/docker-selenium/issues/87
    DBUS_SESSION_BUS_ADDRESS=/dev/null

# Install basics
RUN apt-get update &&  \
    apt-get install -y git wget curl unzip build-essential && \
    curl -o- -L https://yarnpkg.com/install.sh | bash - && \
    apt-get update &&  \
    mkdir source && \
    mkdir -p /root/.cache/yarn/

RUN apt-get install libgtk-3-dev libx11-xcb1 libxss1 libgconf-2-4 libnss3-dev libasound2 libxkbfile1 -y

RUN yarn global add electron@"$ELECTRON_VERSION"

WORKDIR source
CMD ["electron", "."]