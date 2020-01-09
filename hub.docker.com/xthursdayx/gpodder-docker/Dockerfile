FROM lsiobase/guacgui

LABEL maintainer="xthursdayx"

ENV APPNAME="gPodder"
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

RUN \
echo "**** Installing dep packages ****" && \
apt-get update && \
apt-get install -y \
    ca-certificates \
    dbus \
    default-dbus-session-bus \
    ffmpeg \
    gir1.2-gtk-3.0 \
    gir1.2-ayatanaappindicator3-0.1 \
    git \
    jq \
    libgtk-3-dev \
    python3 \
    python3-cairo \
    python3-dbus \
    python3-eyed3 \
    python3-gi \
    python3-gi-cairo \
    python3-html5lib \
    python3-mutagen \
    python3-mygpoclient \
    python3-podcastparser \
    python3-simplejson \
    wget && \
echo "**** Installing gPodder ****" && \
git clone https://github.com/gpodder/gpodder.git && \
cd gpodder && \
python3 tools/localdepends.py && \ 
echo "GPODDER_DOWNLOAD_DIR=/downloads" >> ~/.pam_environment && \
apt-get clean && \
rm -rf \
    /tmp/* \
    /var/lib/apt/lists/* \
    /var/tmp/*
	
COPY root/ /

VOLUME /config
EXPOSE 3389 8080
