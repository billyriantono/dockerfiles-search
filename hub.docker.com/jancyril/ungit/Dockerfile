FROM node:6-alpine

LABEL maintainer="Jan Cyril Segubience <jancyril@segubience.com>"

RUN apk update && apk add --no-cache git openssh openrc tzdata && \
    cp /usr/share/zoneinfo/Asia/Manila /etc/localtime && \
    echo "Asia/Manila" > /etc/timezone && \
    apk del tzdata && \
    rc-update add sshd && npm install ungit -g

EXPOSE 8448

WORKDIR /app

CMD ["ungit"]
