FROM alpine
MAINTAINER Grzegorz Wieczorek <grzewster@gmail.com>
RUN apk add --no-cache nginx uwsgi uwsgi-python py2-pip \
	&& pip2 install --upgrade pip \
	&& pip2 install flask

