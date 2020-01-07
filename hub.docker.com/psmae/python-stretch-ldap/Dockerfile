FROM python:3-stretch

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -qy && \
    apt-get install -y  build-essential python3-dev libldap2-dev libsasl2-dev slapd ldap-utils python-tox lcov valgrind && \
    apt-get clean && \
    pip install --upgrade pip
