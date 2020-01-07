FROM debian:jessie-slim

RUN { set -ex; \
	echo "deb http://ftp.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/bp.list; \
	apt-get update; \
	apt-get install -t jessie-backports --no-install-recommends -y gosu; \
	rm -rf /etc/apt/sources.list.d/bp.list /var/lib/apt/lists/*; \
}
