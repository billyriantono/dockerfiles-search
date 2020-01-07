FROM nimmis/alpine-apache-php7
MAINTAINER Nunurs
LABEL Description="A Simple apache/php image using alpine Linux for Web Apps"

# Setup apache and php
RUN apk --no-cache add \
        bash \
        ffmpeg \
        mkvtoolnix \
        py-pip \
        python

# Install app dependencies
RUN pip install --upgrade pip
RUN pip install Flask
RUN pip install youtube-dl

COPY root/ /web/html/

