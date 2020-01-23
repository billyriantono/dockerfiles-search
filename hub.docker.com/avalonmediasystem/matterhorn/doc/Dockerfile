FROM		autoglass/base
RUN			export DEBIAN_FRONTEND=noninteractive 												&& \
			export TERM=xterm 																	&& \
			apt-get update 																		&& \
			apt-get -y install bind9 netcat 													&& \
			rm /etc/default/bind9 																&& \
			rm /etc/bind/named.conf.options 
ADD			bind9 /etc/default/
ADD			named.conf.options /etc/bind/named.conf.options
RUN			cd /etc/bind/ 																		&& \
			cp rndc.key default.key 															&& \
			dnssec-keygen -a HMAC-MD5 -b 512 -n USER default.key 								&& \
			/bin/bash -c 'mkdir -p /var/bind9/chroot/{etc,dev,var/cache/bind,var/run/named}' 	&& \
			/bin/bash -c 'mv /etc/bind /var/bind9/chroot/etc' 									&& \
			/bin/bash -c 'ln -s /var/bind9/chroot/etc/bind /etc/bind' 							&& \
			cp /etc/localtime /var/bind9/chroot/etc/ 											&& \
			/bin/bash -c 'chmod 775 /var/bind9/chroot/var/{cache/bind,run/named}' 				&& \
			/bin/bash -c 'chgrp bind /var/bind9/chroot/var/{cache/bind,run/named}' 				&& \
			/bin/bash -c 'chown bind:bind /var/bind9/chroot/etc/bind/ -R'
ENV			DEBIAN_FRONTEND=noninteractive
ENV			TERM=xterm
HEALTHCHECK	--interval=1m --timeout=3s CMD nc -zv 127.0.0.1 -u 53 || exit 1
