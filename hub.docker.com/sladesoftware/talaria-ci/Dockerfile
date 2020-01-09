FROM johnnyasantoss/dotnet-mono-docker

# Update the application cache
RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y install sudo

##################################
# NodeJS and Node Package Manager
##################################

# Install NodeJS and npm
RUN curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
RUN apt-get install -y nodejs

# Make sure npm is running as the latest version
RUN npm install -g npm

# Check that npm has been installed
RUN npm -v

###################################
# Chrome
###################################

# The below has been taken from: https://github.com/WeltN24/up-docker-node-chrome-headless/blob/master/Dockerfile

# Get Chrome Sources
RUN curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list

# Install Chrome
RUN apt-get update && apt-get install -y \
    google-chrome-stable \
    --no-install-recommends

###################################
# Yarn
###################################

# Get yarn sources
RUN curl -sSL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb [arch=amd64] https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list

# Install yarn sources
RUN apt-get update && apt-get install -y \
    yarn=1.5.1-1 \
    --no-install-recommends

# Find your desired version here: https://deb.nodesource.com/node_9.x/pool/main/n/nodejs/
# Ubuntu 16.04.3 LTS (Xenial Xerus) (https://wiki.ubuntu.com/Releases)
RUN curl https://deb.nodesource.com/node_9.x/pool/main/n/nodejs/nodejs_9.8.0-1nodesource1_amd64.deb > node.deb \
    && dpkg -i node.deb \
    && rm node.deb
