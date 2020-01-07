# tcloud/python:2.7
# VERSION        0.1

FROM tcloud/base:latest
MAINTAINER tcloud

USER root

RUN yum install -y python-pip python-devel gcc pcre pcre-devel pcre-static && \
	pip install -U pip && \
	pip install uwsgi flask gevent gunicorn requests redis && \
	mkdir -p /data/script

ADD script/start.sh /data/script/start.sh

VOLUME /data

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
ENTRYPOINT ["sh", "-c"]

CMD ["/data/script/start.sh"]
