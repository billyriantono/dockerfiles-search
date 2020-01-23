FROM jleight/phusion-mono:3.12.0
MAINTAINER Jonathon Leight <jonathon.leight@jleight.com>

RUN set -x \
  && apt-get update \
  && apt-get install -y mediainfo libsqlite3-dev libgdiplus libwebp-dev unzip \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
    /tmp/* \
    /var/tmp/*

ENV APP_HOME    /opt/mediabrowser
ENV APP_VERSION master
ENV APP_BASEURL https://github.com/MediaBrowser/MediaBrowser.Releases/raw
ENV APP_PKGNAME MediaBrowser.Mono.zip
ENV APP_URL     ${APP_BASEURL}/${APP_VERSION}/Server/${APP_PKGNAME}

RUN set -x \
  && groupadd -r -g 300 mediabrowser \
  && useradd -r -u 300 -g mediabrowser mediabrowser \
  && mkdir -p "${APP_HOME}" \
  && curl -kL -o /tmp/mb.zip "${APP_URL}" \
  && unzip -d "${APP_HOME}" /tmp/mb.zip \
  && rm -f /tmp/mb.zip \
  && chown -R mediabrowser:mediabrowser "${APP_HOME}"

ADD mediabrowser-service.sh /etc/service/mediabrowser/run

EXPOSE 1900/udp
EXPOSE 7359/udp
EXPOSE 8096/tcp
VOLUME ["/opt/mediabrowser"]