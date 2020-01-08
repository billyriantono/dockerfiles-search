FROM node:latest

# Install deps
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    git \
    python-pip \
    python2.7 \
    python2.7-dev \
    groff-base \
    build-essential \
    xvfb \
    dpkg \
    --no-install-recommends
    
# Get Chrome sources
# RUN curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
#     && echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list

## install ubuntu dependencies
RUN apt-get update \
    && apt-get install -y gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 \
    libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 \
    libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 \
    libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 \
    ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils wget \
    && apt-get install -y python-gobject-2 libappindicator3-1

RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && dpkg -i google-chrome*.deb
# # Install Chrome
# RUN apt-get update && apt-get install -y \
#     google-chrome-stable \
#     --no-install-recommends

# Get yarn sources
RUN curl -sSL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb [arch=amd64] https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list

# Install yarn pinned version
RUN apt-get update && apt-get install -y \
    yarn=1.5.1-1 \
    --no-install-recommends

# # Find your desired version here: https://deb.nodesource.com/node_9.x/pool/main/n/nodejs/
# # Ubuntu 16.04.3 LTS (Xenial Xerus) (https://wiki.ubuntu.com/Releases)
# RUN curl https://deb.nodesource.com/node_9.x/pool/main/n/nodejs/nodejs_9.8.0-1nodesource1_amd64.deb > node.deb \
#  && dpkg -i node.deb \
#  && rm node.deb

# Use non-root user
RUN useradd -ms /bin/bash ci_user
USER ci_user
