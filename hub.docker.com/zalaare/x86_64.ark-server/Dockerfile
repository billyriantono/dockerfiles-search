# -- No Multi-Stage Here; Cleanup at Layer
FROM zalaare/x86_64.steamos:base

# global variables
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
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
# UPGRADE system if needed and INSTALL prerequisits for ARK
#         also install ark-server-tools from FezVrasta, there is no
#         need to re-invent the wheel.
#
##

RUN \
  apt update \
  && apt upgrade -y \
  && apt -y --force-yes install sudo perl-modules \
  && curl -sL http://git.io/vtf5N | reinstall_args=--prefix=/usr bash -s nobody \
  && rm -rf /etc/arkmanager \
  && rm -rf /var/cache/apt/archives/*.deb \
  && rm -rf /var/cache/apt/*.bin \
  && rm -rf /var/lib/apt/lists \
  && rm -rf /usr/share/doc \
  && rm -rf /usr/share/man \
  && mv -v /etc/arkmanager.in /etc/arkmanager \
  && chown 65534:65534 /etc/arkmanager -R

LABEL .maintainer "Zalaare <zalaare@gmail.com>"
LABEL .description "ARK Survival Evolved Game Server"
USER nobody
WORKDIR /steam
ENTRYPOINT ["/init"]
