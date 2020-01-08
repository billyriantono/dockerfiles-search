FROM alpine:3.8
MAINTAINER Vladimir Goldetskyi <goldetsky@gmail.com>

RUN apk add --no-cache python3 python3-dev curl wget gcc make autoconf automake build-base libtool git && \
		python3 -m ensurepip && \
		rm -r /usr/lib/python*/ensurepip && \
		pip3 install --upgrade pip setuptools && \
		if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
		if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
		pip3 install elasticsearch elasticsearch_dsl jq jsonmerge && \
		rm -r /root/.cache
