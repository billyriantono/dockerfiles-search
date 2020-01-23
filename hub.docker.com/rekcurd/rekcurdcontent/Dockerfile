FROM alpine:3.8
RUN apk update
RUN apk add \
        python \
        py-pip \
        build-base \
        gcc \
        python-dev \
        libffi-dev \
        openssl-dev \
        linux-headers
RUN pip install --upgrade pip ansible molecule
WORKDIR /home/root
ENTRYPOINT /usr/bin/molecule
