FROM alpine:3.9

RUN apk update && apk upgrade 
RUN apk add --no-cache rsync openssh-client
RUN rm -rf /var/cache/apk/*
