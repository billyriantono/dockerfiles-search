FROM alpine:3.10

ARG MOUNTEBANK_VERSION=2.1.0
EXPOSE 2525

RUN apk --no-cache add \
        nodejs \
        npm \
    && \
    npm install --global --production \
        mountebank@${MOUNTEBANK_VERSION} \
    && \
    npm cache clean --force \
    && \
    addgroup -g 1000 node \
    && \
    adduser -D -G node -u 1000 node

USER node:node
WORKDIR /home/node
ENTRYPOINT ["mb"]
