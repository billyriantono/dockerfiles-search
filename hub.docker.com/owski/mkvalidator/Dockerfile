FROM alpine
MAINTAINER Josh Grochowski <josh.kastang@gmail.com>

ENV MKVALIDATOR_VERSION 0.5.1
ENV MKVALIDATOR_FILE mkvalidator-$MKVALIDATOR_VERSION.tar.bz2
ENV MKVALIDATOR_DIRECT_URL https://sourceforge.net/projects/matroska/files/mkvalidator/$MKVALIDATOR_FILE
RUN \
	apk --no-cache add \
		ca-certificates \
		openssl \
		build-base \
	&& update-ca-certificates \
	&& wget $MKVALIDATOR_DIRECT_URL -O $MKVALIDATOR_FILE \
	&& tar xf $MKVALIDATOR_FILE \
	&& cd mkvalidator-$MKVALIDATOR_VERSION \
	&& ./configure \
	&& make -C mkvalidator \
	&& make install

VOLUME /data

ENTRYPOINT ["mkvalidator"]
CMD ["--help"]
