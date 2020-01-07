FROM ubuntu:16.04

MAINTAINER Kevin H. Wilson <khwilson@gmail.com>

# Install appropriate locales
ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8
RUN apt-get update && apt-get install -y locales && \
    locale-gen en_US.UTF-8

RUN apt-get install -y software-properties-common vim && \
    add-apt-repository ppa:jonathonf/python-3.6 && \
    apt-get update && \
    apt-get install -y build-essential python3.6 python3.6-dev python3-pip python3.6-venv && \
    apt-get install -y git && \
    rm -rf /var/lib/apt/lists/*

RUN python3.6 -m pip install --upgrade pip wheel
