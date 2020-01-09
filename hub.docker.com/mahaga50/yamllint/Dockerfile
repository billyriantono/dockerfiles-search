# VERSION 1.20.0
# AUTHOR: Maha Gamal
# DESCRIPTION: Basic yamllint container
# BUILD: docker build --rm -t mahaga50/yamllint .
# SOURCE: https://github.com/Mahagamal/docker-yamllint

FROM python:3.7-alpine3.9
LABEL maintainer="MahaGamal"

# Never prompts the user for choices on installation/configuration of packages
ENV DEBIAN_FRONTEND noninteractive
ENV TERM linux

# Yamllint
ARG YAMLLINT_VERSION=1.20.0

ARG PYTHON_DEPS=""

RUN pip install yamllint \
    && if [ -n "${PYTHON_DEPS}" ]; then pip install ${PYTHON_DEPS}; fi 

WORKDIR /workdir

ENTRYPOINT ["yamllint"] # set entrypoint