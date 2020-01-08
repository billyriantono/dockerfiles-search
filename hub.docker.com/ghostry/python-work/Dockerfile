FROM ubuntu:bionic

LABEL maintainer="Ghostry <ghostry.green@gmail.com>"

RUN apt-get update \
  && apt-get install -y software-properties-common \
  && add-apt-repository ppa:deadsnakes/ppa \
  && apt-get install -y git memcached mysql-client libpq-dev python-dev \
  && apt-get install -y python3-pip \
  && apt dist-upgrade -y \
  && apt clean \
  && rm -rf /var/lib/apt/lists/* \
  && pip3 install pipenv

ADD start.sh /start.sh

RUN chmod +x /start.sh \
    && mkdir /data \
    && echo 'export LC_ALL=C.UTF-8;export LANG=C.UTF-8;umask 000;' >> /root/.bashrc

WORKDIR /data

VOLUME ["/data"]

CMD ["/start.sh"]