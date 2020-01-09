# Pull base image.
FROM node:6.11.3-slim
MAINTAINER Scriptwerx <enquiries@scriptwerx.io>

RUN apt-get update && apt-get install -y apt-transport-https libpng12-dev

# Add yarn and dumb-init to sources list
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Add chrome to sources list
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'

# Install bzip2 yarn xvfb chrome
RUN set -x && apt-get update && apt-get install -y bzip2 yarn xvfb google-chrome-stable

# Setup chrome xvfb
# ADD scripts/xvfb-chrome /usr/bin/xvfb-chrome
# RUN ln -sf /usr/bin/xvfb-chrome /usr/bin/google-chrome

# Set chrome env
ENV CHROME_BIN=/usr/bin/google-chrome

# Global install
RUN npm set progress=false && npm i -g phantomjs @angular/cli

# Define working directory.
WORKDIR /workspace