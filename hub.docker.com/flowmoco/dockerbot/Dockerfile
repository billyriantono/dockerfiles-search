FROM alpine:3.8

ARG DOCKER_CLI_VERSION="18.06.0-ce"
ENV DOWNLOAD_URL="https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_CLI_VERSION.tgz"

# install docker client
RUN apk --update add curl \
    && mkdir -p /tmp/download \
    && curl -L $DOWNLOAD_URL | tar -xz -C /tmp/download \
    && mv /tmp/download/docker/docker /usr/local/bin/ \
    && rm -rf /tmp/download \
    && apk del curl \
    && rm -rf /var/cache/apk/*

RUN apk update && apk upgrade && apk add rabbitmq-c-utils bash jq

ADD ./entrypoint.sh /entrypoint.sh
RUN chmod a+x /entrypoint.sh
ADD ./main.sh /main.sh
RUN chmod a+x /main.sh

ENV CONSUME_QUEUE_NAME=docker-tasks
ENV PUBLISH_QUEUE_NAME=docker-tasks
ENV PROXY_SERVICE=proxy-production_haproxy

ENTRYPOINT [ "/entrypoint.sh" ]

