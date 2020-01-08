FROM ubuntu:14.04.4

ENV DEBIAN_FRONTEND noninteractive
ENV UBUNTU_VERSION 14.04.4

RUN apt-get update && \
    apt-get --yes upgrade && \
    apt-get install -y curl ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Install some dependencies that Galaxy users have requested for their apps.  We
# document this list at http://galaxy-guide.meteor.com/base-image-packages.html
# Unfortunately, there's no safe way to upgrade any of these dependencies without
# potentially breaking existing users. We now encourage users to build their
# own custom base image rather than requesting us to install dependencies into
# the default base image.

RUN apt-get update && \
    apt-get install -y rsync phantomjs libpoppler-qt4-dev libcairo2-dev \
      imagemagick libssl-dev wget xfonts-base xfonts-75dpi build-essential \
      gconf-service libasound2 libatk1.0-0 libatk-bridge2.0-0 libc6 libcairo2 \
      libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 \
      libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 \
      libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 \
      libxrandr2 libxrender1 libxss1 libxtst6 ca-certificates fonts-liberation libappindicator1 \
      libnss3 lsb-release xdg-utils graphicsmagick git libjpeg-dev poppler-utils && \
    rm -rf /var/lib/apt/lists/*
