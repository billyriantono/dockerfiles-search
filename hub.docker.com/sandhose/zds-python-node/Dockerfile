FROM node:0.12

RUN apt-get update && apt-get install -y --fix-missing \
	python2.7-dev \
	&& rm -rf /var/lib/apt/lists/*

RUN curl -SL 'https://bootstrap.pypa.io/get-pip.py' | python2
