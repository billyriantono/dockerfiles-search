FROM jenkins
MAINTAINER Vadzim Budzishyn <vadim.budzishyn@gmail.com>

USER root
RUN \
	apt-get update -y && \
	apt-get install -y ffmpeg && \
	apt-get clean && \
	rm -rf \
		/tmp/* \
		/var/lib/apt/lists/* \
		/var/tmp/*

#COPY ./entrypoint.sh /
#RUN chmod +x /entrypoint.sh

USER jenkins

#ENTRYPOINT ["/entrypoint.sh"]
