FROM openjdk:8-alpine

ENV SUBSONIC_UID=1000
ENV SUBSONIC_GID=1000
ENV SUBSONIC_HOME=/srv/subsonic
ENV SUBSONIC_DATA=/subsonic
ENV SUBSONIC_MUSIC=/music
ENV SUBSONIC_PLAYLISTS=/playlists
ENV SUBSONIC_PODCASTS=/podcasts
ENV SUBSONIC_VERSION 6.1.5

ADD https://s3-eu-west-1.amazonaws.com/subsonic-public/download/subsonic-${SUBSONIC_VERSION}-standalone.tar.gz /tmp/subsonic.tar.gz

RUN addgroup -g $SUBSONIC_GID subsonic && \
    adduser -D -H -h $SUBSONIC_HOME -u $SUBSONIC_UID -G subsonic -g subsonic subsonic && \
    mkdir -p $SUBSONIC_HOME && \
    tar zxvf /tmp/subsonic.tar.gz -C $SUBSONIC_HOME && \
    rm -f /tmp/*.tar.gz && \
    chown subsonic $SUBSONIC_HOME && \
    chmod 0770 $SUBSONIC_HOME

RUN mkdir $SUBSONIC_DATA && \
    chown subsonic $SUBSONIC_DATA && \
    chmod 0770 $SUBSONIC_DATA

RUN apk --update add ffmpeg lame

RUN mkdir -p $SUBSONIC_DATA/transcode && \
    ln /usr/bin/ffmpeg /usr/bin/lame $SUBSONIC_DATA/transcode

VOLUME $SUBSONIC_DATA
VOLUME $SUBSONIC_MUSIC
VOLUME $SUBSONIC_PLAYLISTS
VOLUME $SUBSONIC_PODCASTS

EXPOSE 4040
WORKDIR $SUBSONIC_HOME

USER subsonic

CMD java -XX:+UseG1GC \
         -Dsubsonic.home=$SUBSONIC_DATA \
         -Dsubsonic.port=4040 \
         -Dsubsonic.contextPath=/ \
         -Dsubsonic.defaultMusicFolder=$SUBSONIC_MUSIC \
         -Dsubsonic.defaultPodcastFolder=$SUBSONIC_PODCASTS \
         -Dsubsonic.defaultPlaylistFolder=$SUBSONIC_PLAYLISTS \
         -Djava.awt.headless=true \
         -verbose:gc \
         -jar $SUBSONIC_HOME/subsonic-booter-jar-with-dependencies.jar
