# Pull base image.
FROM node:8

# Adapted from @gabrielaraujof/nodejs-gulp-bower

LABEL maintainer "David McRae <david@showpass.com>"

ENV WORKDIR /home/workspace

# Define working directory.
WORKDIR ${WORKDIR}

# Install dependencies
RUN apt-get -yqq update && \
    npm install -g -s gulp bower && \
    npm cache clean --force && \
    apt-get -yqq autoremove && \
    apt-get -yqq clean && \
    rm -rf /var/lib/apt/lists/* /var/cache/* /tmp/* /var/tmp/*

# Allow root for bower
RUN echo '{ "allow_root": true }' > /root/.bowerrc
