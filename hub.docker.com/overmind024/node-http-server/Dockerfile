FROM node:alpine
RUN npm install -g http-server
RUN apk add --update curl && \
    rm -rf /var/cache/apk/*

ENTRYPOINT ["/bin/sh"]