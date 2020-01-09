FROM docker:git

ENV COMPOSE_VERSION 1.24.1

RUN apk update && \
    apk add --no-cache \
	ca-certificates \
	py-pip python-dev \
	libffi-dev \
	openssl-dev \
	gcc \
	libc-dev \
	make \
	curl && \
    pip install "docker-compose${COMPOSE_VERSION:+==}${COMPOSE_VERSION}"

    #wget --output-document=/usr/local/bin/docker-compose https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/run.sh && \
    #chmod +x /usr/local/bin/docker-compose
