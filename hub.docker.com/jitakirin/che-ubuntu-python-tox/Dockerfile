# Based on:
# - https://store.docker.com/community/images/n42org/tox
# - https://github.com/eclipse/che-dockerfiles/blob/master/recipes/ubuntu_python/Dockerfile

FROM eclipse/stack-base:ubuntu

ENV LANG=C.UTF-8
ENV TOX_VERSION 2.9.1

RUN gpg --keyserver keyserver.ubuntu.com --recv-keys 6A755776 \
  && gpg --export 6A755776 | sudo apt-key add - \
  && gpg --keyserver keyserver.ubuntu.com --recv-keys 68854915 \
  && gpg --export 68854915 | sudo apt-key add -

RUN printf '%s\n' \
  'deb http://ppa.launchpad.net/deadsnakes/ppa/ubuntu xenial main' \
  'deb-src http://ppa.launchpad.net/deadsnakes/ppa/ubuntu xenial main' \
  'deb http://ppa.launchpad.net/pypy/ppa/ubuntu xenial main' \
  'deb-src http://ppa.launchpad.net/pypy/ppa/ubuntu xenial main' \
  | sudo tee -a /etc/apt/sources.list >/dev/null

RUN sudo apt-get update \
  && sudo DEBIAN_FRONTEND=noninteractive apt-get install -y \
    git \
    curl \
    python2.3-dev \
    python2.4-dev \
    python2.5-dev \
    python2.6-dev \
    python2.7-dev \
    python3.1-dev \
    python3.2-dev \
    python3.3-dev \
    python3.4-dev \
    python3.5-dev \
    python3.6-dev \
    pypy-dev \
  && sudo rm -rf /var/lib/apt/lists/*

RUN curl -fsSL https://bootstrap.pypa.io/get-pip.py | sudo -H pypy \
  && curl -fsSL https://bootstrap.pypa.io/get-pip.py | sudo -H python2.7 \
  && sudo -H pip install tox==$TOX_VERSION \
  && sudo rm -rf /root/.cache/pip
