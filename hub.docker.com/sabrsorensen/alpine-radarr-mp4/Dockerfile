FROM sabrsorensen/alpine-mono-mp4
MAINTAINER sabrsorensen@gmail.com

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/sabrsorensen/alpine-radarr-mp4.git" \
      org.label-schema.build-date=$BUILD_DATE

# install Radarr
RUN mkdir /radarr && \
    cd /radarr && \
    radarr_tag=$(curl -sX GET "https://api.github.com/repos/Radarr/Radarr/releases" | awk '/tag_name/{print $4;exit}' FS='[""]') && \
    wget "https://github.com/Radarr/Radarr/releases/download/${radarr_tag}/Radarr.develop.${radarr_tag#v}.linux.tar.gz" -O radarr.tar.gz && \
    tar vxzf radarr.tar.gz -C /radarr --strip-components=1 && \
    rm radarr.tar.gz

# add s6-overlay scripts and config
ADD root/ /

# create radarr user
RUN useradd -U -r -m -d /config -s /bin/false radarr

# map /config to host defined config path (used to store configuration from app)
VOLUME /config

# map /data to host defined data path (used to access downloaded as-of-yet-unprocessed media and the imported library)
VOLUME /data

# expose port for http
EXPOSE 7878

ADD healthcheck-radarr.sh /
RUN chmod +x /healthcheck-radarr.sh

HEALTHCHECK --interval=20s --timeout=10s --start-period=60s --retries=5 \
    CMD /healthcheck-radarr.sh
