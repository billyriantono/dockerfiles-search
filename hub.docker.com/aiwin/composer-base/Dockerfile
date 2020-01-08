FROM composer

MAINTAINER Javier Boo "javier.boo@aiwin.es"

RUN set -eux; \
	apk add --update \
	python \
	python-dev \
	py-pip \
	build-base \
	&& rm -rf /var/cache/apk/*

RUN pip install awscli --ignore-installed six && \
	pip install aws-sam-cli && \
	pip install backports.functools_lru_cache

RUN git clone https://github.com/aiwin-tools/devops-scripts.git "$HOME/scripts"