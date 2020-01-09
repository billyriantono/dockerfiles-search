#Alpine 3.8 has the node version (8) and gcc version (6) previously in use
#on CircleCI. However, we should try to run it with newer versions.
#FROM alpine:3.8

FROM alpine:3
RUN apk --no-cache add npm g++ gcc libc-dev make python git openssh-client && \
    delgroup ping && \
    addgroup -g 999 -S drone && \
    adduser -h /drone/src -S -u 999 -G drone drone
