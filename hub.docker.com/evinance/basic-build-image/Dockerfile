FROM buildpack-deps:stretch-scm

RUN apt-get update && \
	apt-get -y install python3-setuptools python3-dev && \
	easy_install3 pip && \
	pip install awscli && \
	apt-get clean