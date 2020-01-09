# -- No Multi-Stage Here; Cleanup at Layer
FROM zalaare/x86_64.steamos:base

# global variables
ENV LC_ALL C
ENV PATH /usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:/bin:/sbin
ENV DEBIAN_FRONTEND noninteractive

# custom init and config template
COPY rootfs /

##
#
# BECOME root
#
##

USER root

##
#
# UPGRADE system if needed and INSTALL prerequisits for DST
#
##

RUN \
  apt update \
  && apt upgrade -y \
  && apt -y --force-yes install libcurl3-gnutls:i386 \
  && rm -rf /var/cache/apt/archives/*.deb \
  && rm -rf /var/cache/apt/*.bin \
  && rm -rf /var/lib/apt/lists \
  && rm -rf /usr/share/doc \
  && rm -rf /usr/share/man

LABEL .maintainer "Zalaare <zalaare@gmail.com>"
LABEL .description "Don't Starve Together Server"
VOLUME ["/mods", "/DST"]
EXPOSE 10999
WORKDIR /steam
USER nobody
ENTRYPOINT ["/init"]
