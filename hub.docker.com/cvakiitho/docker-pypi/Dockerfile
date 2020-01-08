FROM ubuntu:xenial
MAINTAINER Tomas Hartmann <cvakiitho@gmail.com>

RUN apt-get update -qqy && \
    apt-get install python-pip -qqy && \
    pip install --upgrade pip && \
    mkdir -p /srv/pypi

RUN pip install -U passlib pypiserver[cache]==1.2.1

EXPOSE 80
VOLUME ["/srv/pypi"]

ADD entrypoint.sh /
CMD ["/entrypoint.sh"]
