FROM python:3.7-alpine

RUN apk update; \
    apk add \
        git \
        openssh-client \
        openssl \
        curl \
        rsync \
        libsodium \
        libffi \
        musl; \
        pip install --upgrade pip
RUN apk add \
        gcc \
        make \
        libffi-dev \
        musl-dev \
        openssl-dev \
        python-dev; \
    pip install ansible; \
    rm -rf /root/.cache /tmp/*; \
    apk del gcc make libffi-dev musl-dev openssl-dev python-dev
COPY message.sh /usr/local/bin/message.sh
RUN chmod 777 /usr/local/bin/message.sh
