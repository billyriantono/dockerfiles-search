FROM ubuntu:xenial-20170802

LABEL upstream.os.name="ubuntu"
LABEL upstream.os.release="xenial"
LABEL upstream.os.version="20170802"
LABEL maintainer="Martin Migasiewicz <martin.sm@web.de>"

ARG DEBIAN_FRONTEND=noninteractive

COPY apt-conf /etc/apt/apt.conf.d/

# Ensure that locale is set
RUN apt-get update && \
    apt-get install locales

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en

RUN apt-get update && \
    apt-get install \
                python3 \
                python3-pip

RUN pip3 install \
            pip==9.0.1 \
            setuptools==36.2.7

