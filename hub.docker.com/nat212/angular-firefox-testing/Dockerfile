FROM node:alpine
RUN apk --no-cache update && \
        apk --no-cache add --repository http://dl-cdn.alpinelinux.org/alpine/edge/main icu-libs nss freetype && \
        apk --no-cache add openjdk8-jre xvfb ca-certificates && \
        apk --no-cache add --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing firefox
