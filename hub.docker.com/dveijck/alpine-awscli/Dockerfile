FROM alpine:3.8

RUN apk --no-cache update && \
    apk --no-cache add zip && \
    apk --no-cache add git && \
    apk --no-cache add python3 && \
    pip3 install --upgrade pip && \
    pip3 install awscli==1.16.60 && \
    rm -rf /var/cache/apk/*
