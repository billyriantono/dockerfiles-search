FROM side/python:3.7-alpine-pipenv

RUN apk add --no-cache \
	build-base \
        libffi-dev \
        libxml2-dev \
        libxslt-dev \
        libreoffice \
        msttcorefonts-installer \
        fontconfig \
    && update-ms-fonts && fc-cache -f
