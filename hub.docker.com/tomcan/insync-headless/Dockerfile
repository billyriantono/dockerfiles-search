FROM debian:stretch

RUN	apt-get update \
	&& apt-get install -y gpg \
	&& gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv A684470CACCAF35C \
	&& gpg --export --armor A684470CACCAF35C | apt-key add - \
	&& echo deb http://apt.insynchq.com/debian stretch non-free contrib >>/etc/apt/sources.list.d/insync.list \
	&& apt-get update \
	&& apt-get install -y insync-headless \
	&& mkdir /insync

COPY entrypoint.sh /root/entrypoint.sh
RUN chmod +x /root/entrypoint.sh

ENTRYPOINT /root/entrypoint.sh
