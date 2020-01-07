FROM sabrsorensen/alpine-mono
MAINTAINER sabrsorensen@gmail.com

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/sabrsorensen/alpine-mono-mp4.git" \
      org.label-schema.build-date=$BUILD_DATE

# map /config_mp4_automator to host defined sickbeard_mp4_automator config path
VOLUME /config_mp4_automator

# add the edge testing repo and install Radarr/Sonarr and sickbeard_mp4_automator package dependencies
RUN apk -U upgrade --no-cache && \
    apk -U add --no-cache \
        # Sonarr/Radarr dependencies
        libmediainfo \
        # sickbeard_mp4_automator dependencies
        ffmpeg \
        gcc \
        git \
        musl-dev \
        py2-pip \
        py2-setuptools \
        python2 \
        python2-dev

# install sickbeard_mp4_automator PIP packages
RUN pip install --no-cache-dir --upgrade \
        babelfish \
        deluge-client \
        gevent \
        'guessit<2' \
        pip \
        python-dateutil \
        qtfaststart \
        requests \
        requests-cache \
        requests[security] \
        stevedore==1.19.1 \
        'subliminal<2' \
        tmdbsimple

# clone sickbeard_mp4_automator
RUN git clone --depth 1 --single-branch --branch master git://github.com/mdhiggins/sickbeard_mp4_automator /sickbeard_mp4_automator && \
    ln -s /config_mp4_automator/autoProcess.ini /sickbeard_mp4_automator/autoProcess.ini && \
    rm -rf /sickbeard_mp4_automator/post_process && \
    ln -sf /config_mp4_automator/post_process /sickbeard_mp4_automator/
