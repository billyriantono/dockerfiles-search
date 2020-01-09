FROM mba811/debian:latest
MAINTAINER Tsong khapa <ztd811@yahoo.com>
RUN apt-get install -y openssh-server && \
	apt-get clean && \
	echo -n > /var/lib/apt/extended_states
RUN mkdir -p /var/run/sshd
ADD supervisord.conf /etc/supervisor/conf.d/sshd.conf
EXPOSE 22