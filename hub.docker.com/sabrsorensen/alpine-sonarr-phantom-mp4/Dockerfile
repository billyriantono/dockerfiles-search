FROM sabrsorensen/alpine-mono-mp4
MAINTAINER sabrsorensen@gmail.com

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/sabrsorensen/alpine-sonarr-phantom-mp4.git" \
      org.label-schema.build-date=$BUILD_DATE

# install Sonarr V3 "Phantom"
RUN mkdir /sonarr && \
    cd /sonarr && \
    wget "https://services.sonarr.tv/v1/download/phantom-develop/latest?version=3&os=linux" -O sonarr.tar.gz && \
    tar xzvf sonarr.tar.gz -C /sonarr --strip-components=1 && \
    rm sonarr.tar.gz

# add s6-overlay scripts and config
ADD root/ /

# create sonarr user
RUN useradd -U -r -m -d /config -s /bin/false sonarr

# map /config to host defined config path (used to store configuration from app)
VOLUME /config

# map /data to host defined data path (used to access downloaded, unprocessed media and the imported library)
VOLUME /data

# expose port for http
EXPOSE 8989

ADD healthcheck-sonarr.sh /
RUN chmod +x /healthcheck-sonarr.sh

HEALTHCHECK --interval=20s --timeout=10s --start-period=60s --retries=5 \
    CMD /healthcheck-sonarr.sh
