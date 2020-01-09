FROM ubuntu:trusty
MAINTAINER Marcel Grossmann <whatever4711@gmail.com>
LABEL architecture="amd64"

RUN apt-get update \
    && apt-get install -y \
    gcc \
    libffi-dev \
    libssl-dev \
    ovsdbmonitor \
    pyqt4-dev-tools \
    python-dev \
    python-openvswitch \
    python-pip

RUN pip install \
    crypto \
    cryptography \
    pyOpenSSL \
    service_identity \
    twisted \
    zope.interface

ENTRYPOINT ["ovsdbmonitor"]
