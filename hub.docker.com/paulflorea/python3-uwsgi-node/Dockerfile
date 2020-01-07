FROM paulflorea/python3-uwsgi:alpine-test

# Install Node.js and git
RUN apk update && apk upgrade && apk add --no-cache --update \
        nodejs \
        nodejs-npm \
        git \
        && rm -rf /var/cache/apk/* # Delete the cache folder to save some space

# Safely updates NPM
RUN npm install -g npm --prefix=/usr/local
RUN ln -s -f /usr/local/bin/npm /usr/bin/npm 
