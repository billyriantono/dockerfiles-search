FROM mhart/alpine-node:8

# Set newman version 
ENV NEWMAN_VERSION 4.3.1

RUN apk update \
    && apk upgrade \
    && apk add openjdk8 bash \
    && npm install newman --global \
    && rm -rf /var/cache/apk/*
    
# Install newman
RUN npm install -g newman@${NEWMAN_VERSION};
