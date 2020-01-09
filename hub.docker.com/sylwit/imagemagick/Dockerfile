FROM ubuntu:18.10

MAINTAINER sylvain.witmeyer@gmail.com

ARG IMAGEMAGICK_VERSION=7.0.8-12

RUN apt-get update && \
	apt-get install -y \
		libmagickcore-dev \
		libmagickwand-dev \
		libmagic-dev  \
		libopenjp2-tools \
		libopenjp2-7-dev \
		build-essential \
		bc \
		curl \
		vim


RUN curl -o ImageMagick.tar.gz https://imagemagick.org/download/ImageMagick-${IMAGEMAGICK_VERSION}.tar.gz \
	&& tar xvzf ImageMagick.tar.gz

RUN cd ImageMagick-${IMAGEMAGICK_VERSION} \
	&& ./configure \
	&& make \
	&& make install \
	&& ldconfig /usr/local/lib \
	&& rm -f ImageMagick.tar.gz
