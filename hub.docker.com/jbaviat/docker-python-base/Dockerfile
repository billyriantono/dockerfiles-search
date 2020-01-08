# 14.04: LTS Ubuntu (Trusty)

# This is the Python base image.

# TAG: python-base

FROM ubuntu:14.04

MAINTAINER Jean-Baptiste Aviat <jb>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -qyy \
    -o APT::Install-Recommends=false -o APT::Install-Suggests=false \
    python-virtualenv python libffi6 openssl

RUN virtualenv /appenv
RUN . /appenv/bin/activate; pip install pip==7.1.0

