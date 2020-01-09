FROM mhart/alpine-node:4.4.7
RUN apk add gifsicle python make g++ --no-cache --update \
        --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ \
    && npm install --global lwip \
    && apk del python make g++ \
    && cd /usr/lib/node_modules/lwip \
    && rm -Rf tests src
