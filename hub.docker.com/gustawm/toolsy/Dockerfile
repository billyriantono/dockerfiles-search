FROM alpine:latest

ENV PATH="/root/.local/bin:${PATH}"
RUN echo "export PATH=$PATH:/root/.local/bin" > /etc/environment

RUN apk add --update --no-cache bash git gawk less sed grep bc coreutils vim\
  postgresql-client mysql-client openssh-client \
  mtr tcpdump net-snmp-tools curl \
  screen python3 openssl busybox-extras


# aws cli
RUN apk add --update --no-cache python python-dev py-pip build-base \
    && pip install awscli --upgrade --user \
    && apk --purge -v del py-pip \
    && rm -rf /var/cache/apk/*
