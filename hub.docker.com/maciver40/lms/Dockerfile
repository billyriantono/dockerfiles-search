FROM maciver40/ubuntu-base

LABEL maintainer="robert@eisenmann.email"

VOLUME [ "/config" ]
VOLUME [ "/audio" ]

EXPOSE 3483 9090 9000 1900/udp 3483/udp

RUN \
    # INSTALL DEPENDENCIES
    apt-get update && \
    apt-get install -y \
    faad \
    flac \
    lame \
    libgomp1 \
    libio-socket-ssl-perl \
    sox \
    wavpack && \
    # INSTALL LOGITECH MEDIASERVER
    url="http://www.mysqueezebox.com/update/?version=7.9.2&revision=1&geturl=1&os=deb" && \
	latest_lms=$(wget -q -O - "$url") && \
	mkdir -p /sources && cd /sources && \
	wget $latest_lms && \
	lms_deb=${latest_lms##*/} && \
	dpkg -i $lms_deb
