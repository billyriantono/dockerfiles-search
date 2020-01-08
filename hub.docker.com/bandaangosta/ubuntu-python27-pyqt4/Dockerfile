# Dockerfile to build base image for PyQt applications with access to Oracle database
# Ubuntu + Python2.7 + Qt4 + Oracle instantclient

FROM ubuntu:18.04

LABEL maintainer="bandaangosta <jlortiz@uc.cl>"

RUN apt-get update && \
    apt-get install -y python2.7 python-qt4 python-pip unzip libaio1 && \
    pip install --no-cache-dir --upgrade pip && \
# Cleanup
    apt-get -y autoremove && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/* && \
    rm -rf /var/tmp/*

# Following steps are needed for cx_oracle Python library installation and usage
COPY . /installer
WORKDIR /installer

RUN mkdir -p /opt/oracle && \
    unzip ./instantclient-basiclite-linux.x64-18.3.0.0.0dbru.zip -d /opt/oracle/ && \
    unzip ./instantclient-sdk-linux.x64-18.3.0.0.0dbru.zip -d /opt/oracle/ && \
    rm -rf /installer/*

ENV LD_LIBRARY_PATH=/opt/oracle/instantclient_18_3
ENV ORACLE_HOME=/opt/oracle/instantclient_18_3
ENV TNS_ADMIN=/opt/oracle/instantclient_18_3
