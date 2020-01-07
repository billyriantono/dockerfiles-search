FROM sabrsorensen/alpine-mono
MAINTAINER sabrsorensen@gmail.com

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/sabrsorensen/alpine-lidarr.git" \
      org.label-schema.build-date=$BUILD_DATE

# add curl for getting Lidarr tags and fpcalc for audio fingerprinting.
RUN apk -U upgrade && \
    apk -U add --no-cache curl chromaprint

# install Radarr
RUN mkdir /lidarr && \
    cd /lidarr && \
    lidarr_tag=$(curl -sX GET "https://api.github.com/repos/Lidarr/Lidarr/releases" | awk '/tag_name/{print $4;exit}' FS='[""]') && \
    (wget "https://github.com/Lidarr/Lidarr/releases/download/${lidarr_tag}/Lidarr.develop.${lidarr_tag#v}.linux.tar.gz" -O lidarr.tar.gz || \
    wget "https://github.com/Lidarr/Lidarr/releases/download/${lidarr_tag}/Lidarr.master.${lidarr_tag#v}.linux.tar.gz" -O lidarr.tar.gz) && \
    tar vxzf lidarr.tar.gz -C /lidarr --strip-components=1 && \
    rm lidarr.tar.gz

# add s6-overlay scripts and config
ADD root/ /

# create lidarr user
RUN useradd -U -r -m -d /config -s /bin/false lidarr

# map /config to host defined config path (used to store configuration from app)
VOLUME /config

# map /data to host defined data path (used to access downloaded as-of-yet-unprocessed media and the imported library)
VOLUME /data

# expose port for http
EXPOSE 8686

ADD healthcheck-lidarr.sh /
RUN chmod +x /healthcheck-lidarr.sh

HEALTHCHECK --interval=20s --timeout=10s --start-period=60s --retries=5 \
    CMD /healthcheck-lidarr.sh
