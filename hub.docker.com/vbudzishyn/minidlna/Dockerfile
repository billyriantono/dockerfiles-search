FROM ubuntu:18.04
MAINTAINER Vadzim Budzishyn <vadim.budzishyn@gmail.com>

RUN \
	apt-get update -y && \
	apt-get install -y --no-install-recommends minidlna && \
	apt-get clean && \
	rm -rf \
		/tmp/* \
		/var/lib/apt/lists/* \
		/var/tmp/*

COPY ./entrypoint.sh /
RUN chmod +x /entrypoint.sh

EXPOSE 1900 8200

ENTRYPOINT ["/entrypoint.sh"]
