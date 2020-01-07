FROM ubuntu:18.04

MAINTAINER Mahesh Paolini-Subramanya <mahesh@dieswaytoofast.com>


# Ansible and defaults
RUN apt-get update -y && \
    DEBIAN_FRONTEND=noninteractive  \
    apt-get install --no-install-recommends -yq \
    apt-transport-https \
    apt-utils \
    build-essential \
    ca-certificates \
    curl \
    git \
    libffi-dev \
    libssl-dev \
    python-pip \
    python-dev \
    python-yaml \
    libxml2-dev \
    libxslt1-dev \
    rsync \
    software-properties-common \
    zlib1g-dev && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update -y && \
    apt-get install -y ansible && \
    pip install --upgrade awscli \
    boto \
    boto3 \
    credstash \
    jinja2 \
    pycrypto \
    pyyaml \
    shyaml && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /root/.ssh && chmod 700 /root/.ssh
