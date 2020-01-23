FROM ubuntu

MAINTAINER dimkk <dimkk@outlook.com>

ENV NGINX_VERSION 1.11.10

RUN apt-get update && \
	apt-get -y install build-essential \
	libssl-dev nano iptables openvpn procps \
	curl \
	libpcre3 \
	libpcre3-dev && \
	echo '#!/usr/bin/env bash' >/sbin/resolvconf && \
    echo 'conf=/etc/resolv.conf' >>/sbin/resolvconf && \
    echo '[[ -e $conf.orig ]] || cp -p $conf $conf.orig' >>/sbin/resolvconf && \
    echo 'if [[ "${1:-""}" == "-a" ]]; then' >>/sbin/resolvconf && \
    echo '    cat >${conf}' >>/sbin/resolvconf && \
    echo 'elif [[ "${1:-""}" == "-d" ]]; then' >>/sbin/resolvconf && \
    echo '    cat $conf.orig >$conf' >>/sbin/resolvconf && \
    echo 'fi' >>/sbin/resolvconf && \
    chmod +x /sbin/resolvconf && \
	rm -rf /var/lib/apt/lists/* # 20150205

RUN curl -O http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz && \
	tar zxvf nginx-$NGINX_VERSION.tar.gz && \
	cd nginx-$NGINX_VERSION && \
	./configure --with-stream  --with-http_stub_status_module && \
	make && make install

VOLUME /root

COPY ./start.sh /root

WORKDIR /root

CMD /bin/bash ./start.sh