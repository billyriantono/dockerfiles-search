FROM node:6.12.1-alpine

RUN apk --update add g++ make bash zlib-dev libpng-dev git less openssh && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*