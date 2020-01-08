FROM ubuntu:latest
LABEL build="201904291150" maintainer="marc.jakob@bs.ch"

COPY dpkg-excludes /etc/dpkg/dpkg.cfg.d/excludes

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && \
    apt-get -y install \
	krb5-user \
	curl && \
    rm -r /var/log/dpkg.log /var/lib/apt/lists/*

COPY start.sh /
RUN chmod 0750 /start.sh

ENTRYPOINT ["/start.sh"]
