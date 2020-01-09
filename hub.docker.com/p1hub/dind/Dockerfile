FROM docker:19

ENV DIND=1

RUN apk add --no-cache \
		git \
		openssh-client \
		py-pip \
		python-dev \
		libffi-dev \
		openssl-dev \
		gcc \
		libc-dev \
		make \
		bash \
		curl

RUN pip install docker-compose
