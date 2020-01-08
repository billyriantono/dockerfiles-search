# Dockerfile
# Fri Jan 11 16:35:35 -02 2019
#
# Antonio Carlos I. Paes (antonio.paes@sourcefabric.org / www.sourcefabric.org)

FROM ubuntu:18.04

COPY [ "data/", "/tmp/" ]
ENTRYPOINT [ "/docker-entrypoint" ]
ENV TZ Etc/UTC
MAINTAINER Antonio Carlos I. Paes <antonio.paes@sourcefabric.org>

RUN set -x; \
	apt-get -y update && \
	apt-get -y autoremove && \
	apt-get -y dist-upgrade && \
	apt-get -y install "curl" "joe" && \
	install -D -g "root" -m "0755" -o "root" "/tmp/root/docker-entrypoint" "/docker-entrypoint" && \
	mv "/tmp/root/usr/local/scripts" "/usr/local" && \
	rm -fr "/tmp/root"

# EOF