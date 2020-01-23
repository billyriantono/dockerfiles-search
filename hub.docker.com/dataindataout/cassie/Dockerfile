FROM cassandra:latest

LABEL maintainer="Valerie Parham-Thompson" 
LABEL contact="valerie@tortugatech.com" 
LABEL version="2019-11"

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8

RUN apt-get update \
  && apt-get install -y \
  build-essential \
  make \
  git \
  curl \
  wget \
  vim \
  net-tools \
  iputils-ping \
  dnsutils \
  zip \
  unzip \
  ansible \
  python-dev \
  python-openssl \
  libpq-dev libxml2-dev libxslt1-dev libldap2-dev libsasl2-dev libffi-dev libssl-dev libbz2-dev libreadline-dev libsqlite3-dev libncurses5-dev libncursesw5-dev liblzma-dev \
  zlib1g-dev \
  openssh-server \
  sudo \
  llvm \
  ant \
  xz-utils \
  default-jre \
  tk-dev \
  && apt-get clean \ 
  && rm -rf /var/lib/apt/lists/*

RUN wget https://www.python.org/ftp/python/3.7.5/Python-3.7.5.tgz \
&& tar zxf Python-3.7.5.tgz \
&& cd Python-3.7.5/ \
&& ./configure --prefix=/usr/local \
&& make \
&& make install

RUN pip3 install cassandra-medusa
RUN pip3 install cstar

VOLUME "/mnt/data"
CMD ["/bin/bash"]