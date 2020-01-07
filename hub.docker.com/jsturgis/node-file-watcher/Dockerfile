FROM alpine as gitContainer

RUN apk --update add git openssh libtool m4 automake openssl-dev autoconf build-base linux-headers && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

RUN git clone https://github.com/facebook/watchman.git
WORKDIR /watchman/
RUN git checkout v4.9.0 && /bin/bash autogen.sh && \
  /bin/bash configure && \
  make && \
  make install

RUN ls /usr/local/bin

FROM node:alpine

RUN apk --update add git openssl-dev && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

COPY --from=gitContainer /usr/local/bin/watchman /usr/local/bin/watchman
RUN adduser -S jeff
RUN mkdir -p /usr/local/var/run/watchman/jeff-state && chown 100:100 /usr/local/var/run/watchman/jeff-state

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json /usr/src/app/
RUN yarn install --production

# Bundle app source
COPY . /usr/src/app

USER jeff
CMD [ "yarn", "start" ]
