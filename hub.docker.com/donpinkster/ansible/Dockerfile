FROM alpine:latest

ENV ANSIBLE_VERSION 2.5.6

RUN builddeps=' \
		python-dev \
		py2-pip \
		musl-dev \
		openssl-dev \
		libffi-dev \
		gcc \
		' \
	&& apk --no-cache add \
	ca-certificates \
	python \
	py-paramiko \
	py-yaml \
	py-jinja2 \
	py-httplib2 \
    openssh-client \
	$builddeps \
	&& pip install --upgrade pip \
	&& pip install \
		ansible==$ANSIBLE_VERSION \
		six \
	&& apk del --purge $builddeps

WORKDIR /ansible
