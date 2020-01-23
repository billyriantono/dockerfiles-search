FROM ubuntu:latest

RUN apt-get update \
    && apt-get install -y build-essential git libreadline-dev autoconf libssl-dev \
    && rm -r /var/lib/apt/lists/* \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false

ENTRYPOINT ["gcc"]