FROM ubuntu:16.04

MAINTAINER phulm<minhphu1209@gmail.com>

ENV LANG C.UTF-8

RUN DEBIAN_FRONTEND=noninteractive

RUN apt-get update

RUN apt-get install -y postgresql-client-9.5 net-tools apt-utils iputils-ping openssh-server openssh-client nano dialog git\
	libfontconfig zlib1g libfreetype6 libxrender1 libxext6 libx11-6 build-essential python3-dev libxslt-dev libzip-dev libldap2-dev libsasl2-dev virtualenv node-less sudo

RUN apt-get install -y --no-install-recommends ca-certificates curl node-less python3-pip \
        python3-wheel python3-setuptools python3-renderpm python3-watchdog xz-utils \
        libgmp3-dev  libxml2-dev libevent-dev libssl-dev libpq-dev libpng-dev libjpeg-dev
		
RUN curl -L https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.xenial_amd64.deb -o wkhtmltox.deb; \
    dpkg --force-depends -i wkhtmltox.deb; apt-get -y install -f --no-install-recommends;

RUN cd /usr/bin; \
    ln -s pip3 pip; \
    ln -s pydoc3 pydoc; \
    ln -s python3 python;

RUN adduser --disabled-password --gecos "" gitlabci && mkdir -p /data/wms && mkdir /venv