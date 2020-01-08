FROM node:10.10.0-alpine
MAINTAINER Rajesh Jain <rjain15@gmail.com>

RUN mkdir -p /opt
WORKDIR /opt

RUN apk add --no-cache \
	bash \
	openrc \
	ca-certificates \
	curl \
	docker \
	git \
	openssh-client \
	python \
	tar \
	yarn \
	gzip

ENV CLOUDSDK_PYTHON_SITEPACKAGES 1
RUN wget http://dl.google.com/dl/cloudsdk/channels/rapid/google-cloud-sdk.zip && unzip google-cloud-sdk.zip && rm google-cloud-sdk.zip
RUN google-cloud-sdk/install.sh --path-update=true --bash-completion=true --rc-path=/root/.bashrc --additional-components app kubectl

RUN sed -i -- 's/\"disable_updater\": false/\"disable_updater\": true/g' /opt/google-cloud-sdk/lib/googlecloudsdk/core/config.json

RUN mkdir ${HOME}/.ssh
ENV PATH /opt/google-cloud-sdk/bin:$PATH

RUN apk update
RUN rc-update add docker boot
# RUN service docker start

WORKDIR /app
CMD bash
