FROM 0x416e746f6e0a/alpine-base:3.9

# set maintainer label
LABEL MAINTAINER="Anton Chen <contact@antonchen.com>"

RUN \
 echo "**** install build packages ****" && \
 apk add --no-cache --virtual=build-dependencies \
    jq && \
 echo "**** install packages ****" && \
 apk add --no-cache \
    openssl \
    curl \
    findutils \
    py2-pip \
    python \
    tar \
    transmission-cli \
    transmission-daemon \
    unrar \
    unzip && \
 mkdir -p /tmp/twctemp && \
 TWCVERSION=$(curl -sX GET "https://api.github.com/repos/ronggang/transmission-web-control/releases/latest" \
    | jq -r .tag_name ) && \
 curl -o \
    /tmp/twc.tar.gz -L \
    "https://github.com/ronggang/transmission-web-control/archive/${TWCVERSION}.tar.gz" && \
 tar xf \
    /tmp/twc.tar.gz -C \
    /tmp/twctemp --strip-components=1 && \
 mv /tmp/twctemp/src /transmission-web-control && \
 pip install flexget && \
 pip install transmissionrpc && \
 echo "**** cleanup ****" && \
 apk del --purge \
    build-dependencies && \
 rm -rf \
    /tmp/*


# copy local files
COPY root/ /

# ports and volumes
EXPOSE 9091 51413 51413/udp
VOLUME /config /downloads
