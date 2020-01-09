FROM python:3.7-alpine
LABEL maintainer="Mitch Lewandowski <mitch@postoaks.com>"

VOLUME /config

WORKDIR /usr/src/app

# ensure local python is preferred over distribution python
ENV PATH /usr/local/bin:$PATH

ARG TIMEZONE=America/Chicago
ARG UID=10000
ARG GUID=10000
ARG MAKEFLAGS=-j4
ARG VERSION=0.100.2

ADD "https://raw.githubusercontent.com/home-assistant/home-assistant/${VERSION}/requirements_all.txt" /tmp

RUN apk add --update --no-cache libffi-dev libressl-dev nmap iputils curl bluez bluez-dev glib glib-dev libxrandr-dev ffmpeg openzwave && \
    addgroup -g ${GUID} hass && \
    adduser -h /config -D -G hass -s /bin/sh -u ${UID} hass && \
    apk add --update --no-cache --virtual=build-dependencies build-base autoconf linux-headers git tzdata libjpeg-turbo-dev libwebp-dev lcms2-dev libxml2-dev libxslt-dev mariadb-connector-c-dev postgresql-bdr-dev ffmpeg-dev curl-dev cmake swig eudev-dev openzwave-dev && \
    cp "/usr/share/zoneinfo/${TIMEZONE}" /etc/localtime && echo "${TIMEZONE}" > /etc/timezone && \
    # fix for lxml location
    ln -s /usr/include/libxml2/libxml /usr/include/libxml && \
    # newer pip than in the python container, lets grab it
    pip install --no-cache-dir --upgrade pip && \
    # good pre-reqs to have 
    pip install --no-cache-dir mysqlclient psycopg2 cchardet cython && \
	# grab base HASS
    pip install --no-cache-dir homeassistant=="${VERSION}" && \
    #  clean up the container
    apk del build-dependencies && \
    rm -rf /tmp/* /var/tmp/* /var/cache/apk/*

    
EXPOSE 8123
EXPOSE 8300
EXPOSE 51827

ENTRYPOINT ["hass", "--open-ui", "--config=/config"]