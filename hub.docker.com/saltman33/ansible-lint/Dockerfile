FROM python:3.7.3-alpine3.9

LABEL maintainer="Sultan Gillani (sultangillani)"

WORKDIR /playbooks

RUN apk add --no-cache \ 
    linux-headers \
    build-base \
    libffi-dev \
    openssl-dev \
    git \
    openssh \
    && pip install --upgrade pip setuptools wheel ansible-lint \
    && rm -rf /var/cache/apk/* \
    && rm -rf /root/.cache

CMD ["ansible-lint", "--version"]