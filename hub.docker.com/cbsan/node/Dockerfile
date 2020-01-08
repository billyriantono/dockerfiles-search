FROM debian:stretch-slim

LABEL description="Debian Stretch Slim + Node LTS"
LABEL version="10.16.0 LTS"
LABEL maintainer="Cristian B. Santos <cbsan.dev@gmail.com>"

ENV URL_NODE="https://deb.nodesource.com/setup_10.x"

RUN apt update \
    && apt install -y curl \
    && curl -sL "${URL_NODE}" | bash - \
    && apt install -y nodejs --fix-missing

WORKDIR /var/app

CMD ["node"]
