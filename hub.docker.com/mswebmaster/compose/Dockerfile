FROM docker:stable

RUN apk add --update --no-cache \
    bash \
    sudo \
    py-pip \
    python-dev \
    libffi-dev \
    openssl-dev \
    gcc \
    libc-dev \
    make

RUN pip install -U docker-compose

RUN rm -rf /var/lib/apt/lists/*

WORKDIR /src

ENTRYPOINT ["docker-compose"]
