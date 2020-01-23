FROM alpine:3.10

ENV DOCKER_VERSION="19.03.2"
ENV PATH="$PATH:/usr/local/bin"

RUN    apk update \
    && apk add curl python-dev libffi-dev openssl-dev gcc libc-dev make py-pip \
    && rm -rf /var/cache/apk/*

RUN curl -L -o /tmp/docker-$DOCKER_VERSION.tgz https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_VERSION.tgz \
    && tar -xz -C /tmp -f /tmp/docker-$DOCKER_VERSION.tgz \
    && mv /tmp/docker/* /usr/bin

RUN pip install docker-compose
