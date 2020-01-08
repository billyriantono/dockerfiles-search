FROM ubuntu:18.04

MAINTAINER ohartl <hello@ohartl.de>

RUN apt update \
    && apt install software-properties-common -y \
    && apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8 \
    && add-apt-repository 'deb [arch=amd64,arm64,ppc64el] http://mirror.netcologne.de/mariadb/repo/10.2/ubuntu bionic main' -y \
    && apt update \
    && apt install mariadb-client libmysqlclient-dev python3-pip python3-dev -y \
    && cd /usr/local/bin \
    && ln -s /usr/bin/python3 python \
    && ln -s /usr/bin/pip3 pip \
    && pip3 install --upgrade pip \
    && pip3 install virtualenv

VOLUME ["/app"]
WORKDIR /app

CMD ["python3"]
