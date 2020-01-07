FROM ubuntu:18.04

ENV NODE_VERSION 10

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN apt-get update --fix-missing
RUN apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y --no-install-recommends build-essential libssl-dev curl ca-certificates git-core zip

# Step 1 - Install Node
RUN curl -sL "https://deb.nodesource.com/setup_"${NODE_VERSION}".x" | bash -
RUN apt install -y nodejs
RUN node -v

# Setup 2 - Install Node Tools
RUN npm install -g @angular/cli@"^8.x.x"
RUN npm install -g webpack
RUN npm install -g webpack-cli
RUN npm install -g pm2

# Step 3 - Install Cypress Dependencies
RUN apt-get install -y xvfb libgtk2.0-0 libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2

# Step 4 - Test installation
RUN node -v
RUN ng -v
RUN webpack -v
RUN pm2 -v
