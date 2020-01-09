ARG VERSION=latest
FROM archlinux:$VERSION

LABEL description="Archlinux base image" \
	version="1.0"

ENV VERSION $VERSION
RUN echo $VRESION > image_version

ENV container docker
ENV LC_ALL C

# Keep everything up-to-date and remove junk files
RUN ["/usr/bin/pacman", "-Syu", "--quiet", "--noconfirm"]

#Install firewall
RUN ["/usr/bin/pacman", "-S", "nftables", "--quiet", "--noconfirm"]
COPY ./nftables.conf /etc/nftables.conf

# Remove cache
RUN rm -rf /tmp/* /var/tmp/*

# Set a script for startup commands and run it as container's entrypoint
COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
