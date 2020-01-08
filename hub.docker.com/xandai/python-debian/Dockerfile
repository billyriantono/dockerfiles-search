ARG DEBIAN_VERSION=9.8

FROM debian:${DEBIAN_VERSION}

ARG PYTHON3_VERSION='3.5.3-1'

ARG INSTALL_PACKAGES="python3=${PYTHON3_VERSION} python3-pip"

RUN apt-get update &&\
    apt-get install -y --no-install-recommends ${INSTALL_PACKAGES} &&\
    rm -rf /var/lib/apt/lists/* &&\
    ln -s /usr/bin/python3 /usr/bin/python &&\
    ln -s /usr/bin/pip3 /usr/bin/pip &&\
    python -m pip install --upgrade --no-cache-dir --disable-pip-version-check --user pip &&\
    python -m pip install --no-cache-dir setuptools wheel
