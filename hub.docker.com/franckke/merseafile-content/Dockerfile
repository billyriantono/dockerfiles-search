FROM jenkins/jnlp-slave:3.27-1

LABEL maintainer="Chris Yang <chris.yang@spirent.com>"

USER root

ENV PYTHON_VERSION 3

RUN apt-get update \
    && apt-get dist-upgrade -y \
    && apt-get -y install python${PYTHON_VERSION} \
       libffi-dev \
       libpq-dev \
       libssl-dev \
       python3-dev \
       python3-pip \
       python3-setuptools \
       python3-venv \
       python3-wheel \
       build-essential \
    && rm -rf /var/lib/apt/lists/* \
    && ln -nsf /usr/bin/python3 /usr/bin/python

USER jenkins
