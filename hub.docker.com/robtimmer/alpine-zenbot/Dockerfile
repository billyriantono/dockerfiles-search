# Use alpine as base image
FROM alpine

# Set maintainer info
MAINTAINER Rob Timmer <rob@robtimmer.com>

# Set environement variables
ENV GIT_CHECKOUT_HASH="36d8917ffa72e31026d4772ec2331b1684a29f67"

# Install dependencies
RUN apk add --no-cache --update \
    git nodejs nodejs-npm

# Set working directory
WORKDIR /opt/zenbot

# Git clone Zenbot and checkout to the specified hash
RUN git clone https://github.com/carlos8f/zenbot . && \
    git checkout $GIT_CHECKOUT_HASH

# Install Zenbot Node.js dependencies
RUN npm install

# Define volumes
VOLUME ["/opt/zenbot/conf.js"]

# Set entrypoint
ENTRYPOINT ["./zenbot.sh"]
