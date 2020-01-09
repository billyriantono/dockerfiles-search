FROM node:8-alpine

# Add the patch fix
COPY common/stack-fix.c /lib/

# Prepare the libraries packages
RUN set -ex \
    && apk add --no-cache  --virtual .build-deps build-base \
    && gcc  -shared -fPIC /lib/stack-fix.c -o /lib/stack-fix.so \
    && apk del .build-deps

# export the environment variable of LD_PRELOAD
ENV LD_PRELOAD /lib/stack-fix.so

# Update
RUN apk add --update nodejs

WORKDIR /src

# Bundle app source
COPY websocket.io/. /src

# Install app dependencies
#COPY websocket.io/package.json /src/package.json
RUN cd /src; npm install

RUN npm install -g forever

EXPOSE  8000
CMD ["forever", "index.js"]