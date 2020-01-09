FROM debian:jessie

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y \
    wget curl tar \
    python python3 python-pip python-dev \
    make gcc g++ \
    ruby \
    zsh \
    libpq-dev libevent-dev \
    dnsutils \
    postgresql-client \
    vim
RUN pip install pgcli
