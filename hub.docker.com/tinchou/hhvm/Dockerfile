FROM debian:jessie

RUN apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449 && \
	echo deb http://dl.hhvm.com/debian jessie main | tee /etc/apt/sources.list.d/hhvm.list && \
	apt-get update && \
	apt-get -y install hhvm && \
	apt-get -y autoremove && \
	apt-get clean

EXPOSE 9000
CMD ["/usr/bin/hhvm", "--mode", "server", "-vServer.Type=fastcgi", "-vServer.Port=9000"]