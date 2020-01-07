FROM alpine:3.10

LABEL org.label-schema.schema-version="1.0" \
    org.label-schema.name="alpine" \
    org.label-schema.description="alpine 3.10" \
    org.label-schema.version="3.10" \
    org.label-schema.url="https://github.com/dockercraft/alpine" \
    org.label-schema.vendor="Dockercraft (daniel@topdevbox.com)" \
    org.label-schema.license="GPLv2" \
    org.label-schema.build-date="20190917" \
    org.label-schema.docker.cmd.devel="docker build -t alpine ." \
    org.label-schema.docker.cmd="docker run -it --rm alpine /bin/sh"

RUN apk update \
	&& apk upgrade \
	&& rm -rf /var/cache/apk/*
