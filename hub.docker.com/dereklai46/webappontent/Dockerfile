FROM node:11-alpine
RUN apk add --update git && \
    apk add --update openssh && \
    apk add --update bash && \
    apk add --update make && \
    apk add --update curl && \
    apk add --update python2 && \
    apk add --update gcc && \
    apk add --update coreutils && \
    apk add --update bc && \
    apk add --update g++ && \
    apk add --update jq && \
    apk add --update openjdk8 && \
    rm -rf /tmp/* /var/cache/apk/*

ENV PATH="/usr/lib/jvm/default-jvm/bin/:${PATH}"
