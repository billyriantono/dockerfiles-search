FROM node:7-alpine

RUN apk update
RUN apk add python python-dev py-pip build-base

RUN node --version && \
	npm --version && \
	python --version && \
	pip --version

RUN echo "@community http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories

RUN apk add --update --no-cache ca-certificates gcc g++ curl openblas-dev@community

RUN ln -s /usr/include/locale.h /usr/include/xlocale.h

RUN pip install --no-cache-dir --disable-pip-version-check numpy==1.13.0rc1
RUN pip install --no-cache-dir --disable-pip-version-check scipy==0.19.0
RUN pip install --no-cache-dir --disable-pip-version-check scikit-learn==0.17.1

