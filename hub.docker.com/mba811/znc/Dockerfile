FROM mba811/debian:latest
MAINTAINER Tsong khapa <ztd811@yahoo.com>
CMD /bin/sh -c apt-get install -y znc && \
	apt-get clean && \
	echo -n > /var/lib/apt/extended_states
ADD supervisord.conf /etc/supervisor/conf.d/znc.conf
EXPOSE 6667
EXPOSE 6697