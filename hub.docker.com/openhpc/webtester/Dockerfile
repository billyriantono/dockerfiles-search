FROM alpine:latest

LABEL name="WebTester" \
    vendor="ClusterTech" \
    version="1" \
    maintainer="jggao@clustertech.com"

ENV PATH /usr/local/bin:$PATH

ENV LANG zh_CN.UTF-8

RUN apk add --update --no-cache ca-certificates bash python3 python3-dev jpeg-dev zlib-dev

RUN set -ex; \
    cd /usr/bin \
	&& ln -svf pydoc3 pydoc \
	&& ln -svf python3 python \
	&& ln -svf python3-config python-config \
	&& ln -svf pip3 pip

RUN set -ex; \
    \
    apk add --update --no-cache --virtual .deps gcc g++; \
	\
	pip --version; \
	\
	pip install selenium behave IPython nose pillow; \
	\
	apk del .deps

CMD 'bash'
