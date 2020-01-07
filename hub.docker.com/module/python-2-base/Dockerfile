FROM ubuntu:14.04
MAINTAINER Carl Robben <carl@module.net.nz>

RUN apt-get update

RUN \
  apt-get install -y \
  build-essential \
  curl \
  wget \
  git

RUN \
  apt-get build-dep -y \
  python-dev \
  python-imaging \
  python-psycopg2

RUN \
  apt-get install -y \
  python-dev \
  python-imaging \
  libssl-dev \
  libxml2-dev \
  libpq-dev \
  libproj-dev \
  libxslt1-dev \
  libffi-dev \
  postgresql-client \
  python-psycopg2 \
  zlib1g-dev && \
  rm -rf /var/lib/apt/lists/*

ADD https://bootstrap.pypa.io/get-pip.py /tmp/get-pip.py
RUN python /tmp/get-pip.py



CMD ["bash"]


