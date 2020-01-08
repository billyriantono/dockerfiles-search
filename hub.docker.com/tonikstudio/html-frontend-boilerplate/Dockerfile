FROM tonikstudio/base:latest

RUN echo "@edge http://nl.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories \
    && apk add --update \
        libuv@edge \
        nodejs@edge \
        nodejs-npm@edge \
    && rm -rf /var/cache/apk/*

CMD ["npm"]
