FROM plexinc/pms-docker

ARG S6_OVERLAY_VERSION=v1.17.2.0
ARG DEBIAN_FRONTEND="noninteractive"
ENV TERM="xterm" LANG="C.UTF-8" LC_ALL="C.UTF-8"

ENTRYPOINT ["/init"]

RUN apt-get update && \
    apt-get install -y \
    xmlstarlet \
    uuid-runtime \
    build-essential \
    software-properties-common \
    python-software-properties \
    curl \
    git \
    unzip \
    screen \
    nano \
    ffmpeg \
    libsdl1.2-dev \
    autoconf \
    libtool \
    libavutil-dev \
    libavformat-dev \
    libavcodec-dev \
    libargtable2-dev

RUN apt-get -y dist-upgrade

#Add Handbrake and Mkvtoolnix
RUN add-apt-repository ppa:stebbins/handbrake-releases && \
    add-apt-repository ppa:djcj/mkvtoolnix  && \
    apt-get update && \
    apt-get install -y mkvtoolnix handbrake-cli

#Add Comskip
RUN git clone https://github.com/erikkaashoek/Comskip.git
RUN cd Comskip && \
    ./autogen.sh && \
    ./configure && \
    make && \
    make install &&\
    cd / && \
    rm -rf Comskip

# Cleanup
RUN apt-get -y autoremove && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/* && \
    rm -rf /var/tmp/*

#download and unzip Webtools
RUN \
    curl -J -L -o /tmp/WebTools.bundle.zip https://github.com/ukdtom/WebTools.bundle/releases/download/2.4.1/WebTools.bundle.zip && \
      unzip /tmp/WebTools.bundle.zip -d /Webtools

# Fetch and extract S6 overlay
RUN \
    curl -J -L -o /tmp/s6-overlay-amd64.tar.gz https://github.com/just-containers/s6-overlay/releases/download/${S6_OVERLAY_VERSION}/s6-overlay-amd64.tar.gz && \
    tar xzf /tmp/s6-overlay-amd64.tar.gz -C /

# Setup directories
RUN \
    mkdir -p \
      /config \
      /transcode \
      /data

EXPOSE 32400/tcp 3005/tcp 8324/tcp 32469/tcp 1900/udp 32410/udp 32412/udp 32413/udp 32414/udp
VOLUME /config /transcode

ENV CHANGE_CONFIG_DIR_OWNERSHIP="true" \
    HOME="/config"

ARG TAG=plexpass
ARG URL=

COPY root/ /

RUN \
# Save version and install
    /installBinary.sh

HEALTHCHECK --interval=200s --timeout=100s CMD /healthcheck.sh || exit 1


ENV LOG_DIR="/config/Library/Application Support/Plex Media Server/Logs/" \
    PLEX_DVR_TV_DIR="/data/media/TV"

LABEL org.freenas.interactive="false"       \
      org.freenas.version="1.4.4.3495"      \
      org.freenas.upgradeable="true"        \
      org.freenas.expose-ports-at-host="true"   \
      org.freenas.autostart="true"      \
      org.freenas.capabilities-add="NET_BROADCAST" \
      org.freenas.web-ui-protocol="http"    \
      org.freenas.web-ui-port=32400     \
      org.freenas.web-ui-path="web"     \
      org.freenas.port-mappings="32400:32400/tcp,3005:3005/tcp,8324:8324/tcp,32469:32469/tcp,1900:1900/udp,32410:32410/udp,32412:32412/udp,32413:32413/udp,32414:32414/udp"         \
      org.freenas.volumes="[                    \
          {                         \
              \"name\": \"/config\",                \
              \"descr\": \"Config storage space\"       \
          },                            \
          {                         \
              \"name\": \"/transcode\",             \
              \"descr\": \"Video transcode directory\"      \
          },                            \
          {                         \
              \"name\": \"/data\",              \
              \"descr\": \"Media volume\"           \
          }                         \
      ]"                            \
      org.freenas.settings="[                   \
          {                         \
              \"env\": \"TZ\",                  \
              \"descr\": \"Plex container Timezone\",       \
              \"optional\": true                \
          },                            \
          {                         \
              \"env\": \"ADVERTISE_IP\",            \
              \"descr\": \"http://<hostIPAddress>:32400/\", \
              \"optional\": true                \
          },                            \
          {                         \
              \"env\": \"ALLOWED_NETWORKS\",            \
              \"descr\": \"IP/mask[,IP/mask]\",         \
              \"optional\": true                \
          },                            \
          {                         \
              \"env\": \"PLEX_UID\",                \
              \"descr\": \"Plex User ID\",          \
              \"optional\": true                \
          },                            \
          {                         \
              \"env\": \"PLEX_GID\",                \
              \"descr\": \"Plex Group ID\",         \
              \"optional\": true                \
          },                            \
          {                         \
              \"env\": \"PLEX_CLAIM\",              \
              \"descr\": \"Plex Account Token\",        \
              \"optional\": true                \
          },                             \
          {             \
              \"env\": \"PLEX_DVR_TV_DIR\",        \
              \"descr\": \"/data/media/TV\",    \
              \"optional\": true        \
          }               \
      ]"



VOLUME /customscripts /PATH/TO/HOST/DIR
ENV PATH /customscripts/bin:$PATH

#
#Add scripts
COPY convert.sh /usr/bin/convert.sh
COPY comcut /usr/local/bin/comcut
COPY comchap /usr/local/bin/comchap
COPY post_encode.sh /usr/bin/post_encode.sh
COPY dvr.sh /usr/local/bin/dvr.sh
COPY PlexComskip.py /usr/local/bin/PlexComskip.py
COPY PlexComskip.conf /usr/local/bin/PlexComskip.conf
COPY post_no_encode.sh /usr/bin/post_no_encode.sh
COPY post_encode_only.sh /usr/bin/post_encode_only.sh
COPY comskip.ini /usr/local/etc/comskip.ini

RUN chmod +x /usr/bin/post_encode_only.sh
RUN chmod +x /usr/bin/post_no_encode.sh
RUN chmod +x /usr/local/bin/PlexComskip.py
RUN chmod +x /usr/local/bin/dvr.sh
RUN chmod +x /usr/bin/convert.sh
RUN chmod +x /usr/local/bin/comcut
RUN chmod +x /usr/local/bin/comchap
RUN chmod +x /usr/bin/post_encode.sh
RUN touch /tmp/comchap.log