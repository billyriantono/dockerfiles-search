ARG VERSION=latest
FROM ubuntu:$VERSION

LABEL description="Archlinux base image" \
	version="1.0"

ENV VERSION $VERSION
RUN echo $VRESION > image_version

ENV container docker
ENV LC_ALL C

# Keep everything up-to-date and remove junk files
RUN ["/usr/bin/apt-get", "update", "--quiet", "--yes"]
RUN ["/usr/bin/apt-get", "upgrade", "--quiet", "--yes"]
RUN ["/usr/bin/apt-get", "install", "apt-utils", "netbase" ,"--quiet", "--yes"]

#Install firewall
RUN ["/usr/bin/apt-get", "install", "nftables", "--quiet", "--yes"]
COPY ./nftables.conf /etc/nftables.conf

# Remove cache
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set a script for startup commands and run it as container's entrypoint
COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]