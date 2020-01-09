FROM node:10-alpine

RUN mkdir /app
WORKDIR /app

# INSTALL_CHROME
# Install dependencies required for chrome and puppeteer
ENV CHROME_BIN="/usr/bin/chromium-browser"\
        PUPPETEER_SKIP_CHROMIUM_DOWNLOAD="true"
    
RUN set -x \
  && apk update \
  && apk upgrade \
  # replacing default repositories with edge ones
  && echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" > /etc/apk/repositories \
  && echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
  && echo "http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories \
  \
  # Add the packages
  && apk add --no-cache dumb-init curl make gcc g++ python linux-headers binutils-gold gnupg libstdc++ nss chromium \
  \
  # Do some cleanup
  && apk del --no-cache make gcc g++ python binutils-gold gnupg libstdc++ \
  && rm -rf /usr/include \
  && rm -rf /var/cache/apk/* /root/.node-gyp /usr/share/man /tmp/* \
  && echo
# /INSTALL_CHROME

ADD package.json /app/package.json
RUN npm install

ADD tsconfig.json /app/tsconfig.json
ADD nodemon.json /app/nodemon.json

ADD src/. /app/src


# If building for production
# - build babel to dist folder
# - remove dev dependencies
ARG env=production
ADD scripts/build_production.sh /build_production.sh
RUN if [ "${env}" = "production" ] ; then sh /build_production.sh ; fi


EXPOSE 3000
CMD npm start
