FROM alpine
MAINTAINER Quan To <btquanto@gmail.com>

# basic flask environment
RUN apk add --no-cache \
		bash \
		git \
		py2-pip \
		build-base \
		python-dev \
		libffi-dev \
	&& pip2 install --upgrade pip \
	&& pip install gunicorn==19.6.0 flask==0.12

# Variables
ENV APP_DIR /src
ENV APP_MODULE app
ENV APP_INSTANCE app

# app dir
RUN mkdir ${APP_DIR}
WORKDIR ${APP_DIR}

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]
