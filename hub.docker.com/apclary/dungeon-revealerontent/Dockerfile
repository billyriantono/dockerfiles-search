FROM lsiobase/alpine:3.7

# set version label
ARG BUILD_DATE
ARG VERSION
LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"
LABEL maintainer="sparklyballs"

# copy patches
COPY patches/ /defaults/patches/

# install packages
RUN \
 echo "**** install packages ****" && \
 apk add --no-cache -U \
	ca-certificates \
	curl \
	fcgi \
	ffmpeg \
	geoip \
	gzip \
	irssi \
	irssi-perl \
	logrotate \
	mediainfo \
	nginx \
	perl \
	perl-archive-zip \
	perl-digest-sha1 \
	perl-html-parser \
	perl-json \
	perl-net-ssleay \
	perl-xml-libxml \
  python3 \
	php7 \
	php7-cgi \
	php7-fpm \
	php7-json \
	php7-mbstring \
	php7-pear \
	php7-sockets \
	rtorrent \
	screen \
	sox \
	tar \
	unrar \
	unzip \
	wget \
	git \
	zlib \
	zip && \
 apk add --no-cache -U --repository http://nl.alpinelinux.org/alpine/edge/testing \
	perl-json-xs && \
 echo "**** setup python pip dependencies ****" && \
 python3 -m pip install --no-cache-dir -U pip setuptools requests urllib3 && \
 echo "**** install webui ****" && \
 mkdir -p \
	/usr/share/webapps/rutorrent \
	/defaults/rutorrent-conf && \
 curl -o \
	/tmp/rutorrent.tar.gz -L \
	"https://github.com/Novik/ruTorrent/archive/master.tar.gz" && \
 tar xf \
	/tmp/rutorrent.tar.gz -C \
	/usr/share/webapps/rutorrent --strip-components=1 && \
 mv /usr/share/webapps/rutorrent/conf/* \
	/defaults/rutorrent-conf/ && \
 rm -rf \
	/defaults/rutorrent-conf/users && \
 echo "**** patch snoopy.inc for rss fix ****" && \
 cd /usr/share/webapps/rutorrent/php && \
 patch < /defaults/patches/snoopy.patch && \
 echo "**** install additional rutorrent theme ****" && \
 git clone git://github.com/phlooo/ruTorrent-MaterialDesign.git /usr/share/webapps/rutorrent/plugins/theme/themes/MaterialDesign && \
 echo "**** fix logrotate ****" && \
 sed -i "s#/var/log/messages {}.*# #g" /etc/logrotate.conf && \
 echo "**** cleanup ****" && \
 rm -rf \
	/etc/nginx/conf.d/default.conf \
	/tmp/*

# add local files
COPY root/ /

ENV \
  S6_KILL_GRACETIME=60000

# ports and volumes
EXPOSE 80
VOLUME /config /downloads
