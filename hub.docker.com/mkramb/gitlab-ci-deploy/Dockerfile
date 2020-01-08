FROM smebberson/alpine-nginx-nodejs:4.2.2

# install build tools
RUN \
  apk add --update \
	build-base

# install python dev tools
RUN \
  apk add --update \
	python \
	python-dev \
	py-pip

# install dumb-init from source
RUN pip install dumb-init
