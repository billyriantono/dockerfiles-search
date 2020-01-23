FROM drbroiler/alpine

MAINTAINER github@drbroiler.de

ENV SUBSONIC_UID=1000
ENV SUBSONIC_GID=1000
ENV SUBSONIC_HOME=/usr/share/subsonic
ENV SUBSONIC_DATA=/var/subsonic
ENV SUBSONIC_VERSION 6.1.5

ADD https://s3-eu-west-1.amazonaws.com/subsonic-public/download/subsonic-${SUBSONIC_VERSION}-standalone.tar.gz /tmp/subsonic.tar.gz

RUN addgroup -g $SUBSONIC_GID subsonic && \
    adduser -D -H -h $SUBSONIC_HOME -u $SUBSONIC_UID -G subsonic -g "SubsonicUser" subsonic && \
    mkdir -p $SUBSONIC_HOME && \
    tar zxvf /tmp/subsonic.tar.gz -C $SUBSONIC_HOME && \
    rm -f /tmp/*.tar.gz && \
    chown subsonic $SUBSONIC_HOME && \
    chmod 0770 $SUBSONIC_HOME

RUN mkdir $SUBSONIC_DATA && \
    chown subsonic $SUBSONIC_DATA && \
    chmod 0770 $SUBSONIC_DATA

RUN apk --update add openjdk8-jre ffmpeg

RUN mkdir -p $SUBSONIC_DATA/transcode && \
    ln /usr/bin/ffmpeg /usr/bin/lame $SUBSONIC_DATA/transcode

VOLUME $SUBSONIC_DATA

EXPOSE 4040

USER subsonic

COPY start.sh /start.sh

CMD []
ENTRYPOINT ["/start.sh"]
