FROM lsiobase/alpine:3.10

ARG VERSION="0.9"
ARG DATE="2020/01/06"
LABEL build_version="rtorrent-autodl version:- ${VERSION}, ${DATE}"
LABEL maintainer="tsubus"

# set environment variables
ENV HOME="/config/rtorrent-autodl"

# copy patches
COPY patches/ /defaults/patches/

# volume
VOLUME /config /media

# install packages
RUN \
 echo "**** install nginx packages ****" && \
 apk update && \
 apk add --no-cache \
	apache2-utils \
	git \
	libressl2.7-libssl \
	logrotate \
	nano \
	nginx \
	openssl \
	php7 \
	php7-fileinfo \
	php7-fpm \
	php7-json \
	php7-mbstring \
	php7-openssl \
	php7-session \
	php7-simplexml \
	php7-xml \
	php7-xmlwriter \
	php7-zlib && \
 echo "**** configure nginx ****" && \
 echo 'fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;' >> \
	/etc/nginx/fastcgi_params && \
 rm -f /etc/nginx/conf.d/default.conf && \
 echo "**** fix logrotate ****" && \
 sed -i "s#/var/log/messages {}.*# #g" /etc/logrotate.conf && \
 sed -i 's#/usr/sbin/logrotate /etc/logrotate.conf#/usr/sbin/logrotate /etc/logrotate.conf -s /config/log/logrotate.status#g' \
	/etc/periodic/daily/logrotate

RUN \
 echo "**** install rutorrent packages ****" && \
 apk add --no-cache --virtual=build-dependencies \
	g++ \
	libffi-dev \
	make \
	musl \
	openssl-dev \
	python3-dev && \
 echo "**** install runtime packages ****" && \
 apk add --no-cache --upgrade \
	bind-tools \
	curl \
	fcgi \
	ffmpeg \
	geoip \
	gzip \
	libffi \
	mediainfo \
	openssl \
	php7 \
	php7-curl \
	php7-cgi \
	php7-pear \
	php7-zip \
	procps \
	python3 \
	rtorrent \
	screen \
	sox \
	unrar \
	zip && \
 echo "**** install pip packages ****" && \
 pip3 install --no-cache-dir -U \
	cfscrape \
	cloudscraper && \
 echo "**** install rutorrent ****" && \
 RUTORRENT_RELEASE=$(curl -sX GET "https://api.github.com/repos/Novik/ruTorrent/releases/latest" \
	| awk '/tag_name/{print $4;exit}' FS='[""]') && \
 curl -o \
 /tmp/rutorrent.tar.gz -L \
	"https://github.com/Novik/rutorrent/archive/${RUTORRENT_RELEASE}.tar.gz" && \
 mkdir -p \
	/app/rutorrent \
	/defaults/rutorrent-conf && \
 tar xf \
 /tmp/rutorrent.tar.gz -C \
	/app/rutorrent --strip-components=1 && \
 mv /app/rutorrent/conf/* \
	/defaults/rutorrent-conf/ && \
 rm -rf \
	/defaults/rutorrent-conf/users && \
 echo "**** patch snoopy.inc for rss fix ****" && \
 cd /app/rutorrent/php && \
 patch < /defaults/patches/snoopy.patch && \
 echo "**** install autodl-irssi rutorrent plugin ****" && \
 apk add --no-cache --upgrade \
    php7-sockets \
    git \
    zlib && \
 git clone --depth 1 --single-branch \
    https://github.com/autodl-community/autodl-rutorrent.git \
    /app/rutorrent/plugins/autodl-irssi && \
 echo "**** install irssi and autodl ****" && \
 # Autodl dependencies from edge
 apk add --no-cache --repository http://nl.alpinelinux.org/alpine/edge/main \
    perl \
    perl-dev \
    perl-utils \
    perl-archive-zip \
    perl-net-ssleay \
    perl-html-parser \
    perl-digest-sha1 \
    perl-json \
    irssi \
    irssi-perl && \
 apk add --no-cache --repository http://nl.alpinelinux.org/alpine/edge/community \
    perl-xml-libxml && \
 PERL_MM_USE_DEFAULT=1 cpan JSON::XS && \
 git clone --depth 1 --single-branch \
     https://gitlab.com/tylagat/autodl-curl-sonarr.git \
     /app/autodl-curl-sonarr && \
 echo "**** cleanup ****" && \
 apk del --purge \
	build-dependencies && \
 rm -rf \
	/etc/nginx/conf.d/default.conf \
	/root/.cache \
	/tmp/*

# add local files
COPY root/ /
