FROM python:3.7-alpine3.10

LABEL maintainer="Viddsee <developer@viddsee.com>"

ENV VERSION 3.0.2

WORKDIR /opt

RUN apk update && apk upgrade && \
    apk add --no-cache git

RUN cd /opt \
	&& git clone -b ${VERSION} --single-branch https://opendev.org/jjb/jenkins-job-builder.git \
	&& cd /opt/jenkins-job-builder \
	&& pip install -r requirements.txt \
	&& python setup.py install \
	&& mkdir /.cache && chmod 777 /.cache \
	&& rm -R /opt/jenkins-job-builder
