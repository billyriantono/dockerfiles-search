FROM alpine:latest

RUN apk --no-cache --update add lftp ca-certificates openssh bash \
	php5-cli \
    php5-json \
	tree \
    python \
    python-dev \
    py-pip \
    php-ctype \
    build-base \
    git \
    && rm -rf /var/cache/apk/* \
    && git clone https://github.com/Gallore/yaml_cli \
    && cd yaml_cli \
    && pip install . \
    && cd .. \
    && rm -R yaml_cli

ENTRYPOINT []
CMD ["--help"]
