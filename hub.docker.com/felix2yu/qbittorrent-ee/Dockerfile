
FROM alpine as compilingqB

#compiling qB

ARG  LIBTORRENT_VER=1.2.3
ARG  QBITTORRENTEE_VER=4.2.1.10


RUN  apk add --no-cache ca-certificates make g++ gcc qt5-qtsvg-dev boost-dev qt5-qttools-dev file \
&&   mkdir /qbtorrent  \
&&   wget -P /qbtorrent https://github.com/arvidn/libtorrent/releases/download/libtorrent-`echo "$LIBTORRENT_VER"|sed 's#\.#_#g'`/libtorrent-rasterbar-${LIBTORRENT_VER}.tar.gz   \
&&   tar  -zxvf  /qbtorrent/libtorrent-rasterbar-${LIBTORRENT_VER}.tar.gz   -C    /qbtorrent  \
&&   cd  /qbtorrent/libtorrent-rasterbar-${LIBTORRENT_VER} \
&&   ./configure  --host=x86_64-alpine-linux-musl \
&&   make install-strip \
&&   wget  -P /qbtorrent https://github.com/c0re100/qBittorrent-Enhanced-Edition/archive/release-${QBITTORRENTEE_VER}.zip   \
&&   unzip   /qbtorrent/release-${QBITTORRENTEE_VER}.zip  -d    /qbtorrent \
&&   cd  /qbtorrent/qBittorrent-Enhanced-Edition-release-${QBITTORRENTEE_VER} \
&&   ./configure   --disable-gui --host=x86_64-alpine-linux-musl \
&&   make install \
&&   ldd /usr/local/bin/qbittorrent-nox   |cut -d ">" -f 2|grep lib|cut -d "(" -f 1|xargs tar -chvf /qbtorrent/qbittorrent.tar  \
&&   mkdir /qbittorrent   \
&&   tar  -xvf /qbtorrent/qbittorrent.tar   -C  /qbittorrent   \
&&   cp --parents /usr/local/bin/qbittorrent-nox  /qbittorrent  \
&&   wget -O /tmp/ipfilter.dat https://github.com/c0re100/qBittorrent-Enhanced-Edition/releases/download/release-4.1.9.15/ipfilter.dat
 

 # docker qB


FROM alpine

ARG S6_VER=1.22.1.0

ENV TRACKERSAUTO=YES
ENV TZ=Asia/Shanghai
ENV WEBUIPORT=8989

COPY root /
COPY --from=compilingqB  /qbittorrent  /

# install bash curl caddy tzdata s6 overlay python3
RUN  wget --no-check-certificate https://github.com/just-containers/s6-overlay/releases/download/v${S6_VER}/s6-overlay-amd64.tar.gz  \
&&   tar -xvzf s6-overlay-amd64.tar.gz  \
&&   rm s6-overlay-amd64.tar.gz   \
&&   apk add --no-cache bash curl ca-certificates tzdata python3 \
&&   chmod a+x  /usr/local/qbittorrent/updatetrackers.sh  \
&&   chmod a+x  /usr/local/bin/qbittorrent-nox  \
&&   mkdir -p /root/.config/qBittorrent

COPY --from=compilingqB  /tmp/ipfilter.dat /root/.config/qBittorrent

VOLUME /Downloads /config
EXPOSE 8989  6881  6881/udp
ENTRYPOINT [ "/init" ]
