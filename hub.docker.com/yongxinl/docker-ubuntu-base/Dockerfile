# =============================================================================
#
# Dockerfile    Dockerfile
#
# - by George Li <yongxinl@outlook.com>.
# - Date: Dec 2015
#
# =============================================================================

# -----------------------------------------------------------------------------
# Base image
# -----------------------------------------------------------------------------
FROM ubuntu:latest
MAINTAINER George Li <yongxinl@outlook.com>

# -----------------------------------------------------------------------------
# Environment and Working directory
# -----------------------------------------------------------------------------
ENV ROOT_PATH="/data"
ENV DEBIAN_FRONTEND=noninteractive \
    LC_ALL="C.UTF-8" \
    LANG="en_US.UTF-8" \
    LANGUAGE="en_US.UTF-8" \
    TERM=xterm \
    SU_USER=_===USERNAME===_ \
    SU_GROUP=_===USERGROUP===_

# -----------------------------------------------------------------------------
# Base Install
# -----------------------------------------------------------------------------
# - Install basic packages
# - Install inotify, needed to automate daemon restarts after config file changes
# - Install supervisor for process manager
RUN RUNTMDEPS="ca-certificates curl inotify-tools nano supervisor unzip wget" \
  && FUNCSDEPS="" \
  && apt-get --quiet --yes update \
  && apt-get --quiet --yes upgrade \
  && apt-get --yes install --no-install-recommends ${RUNTMDEPS} ${FUNCSDEPS} \
  && apt-get --yes autoremove \
  && apt-get --yes clean \
  && echo -n > /var/lib/apt/extended_states \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /var/lib/{cache,log} /var/log/* \
  && rm -rf /tmp/*

# -----------------------------------------------------------------------------
# Configure files
# -----------------------------------------------------------------------------
ADD assets /etc
RUN chmod +x /etc/bootstrap.sh

# -----------------------------------------------------------------------------
# Ports exposed to host
# -----------------------------------------------------------------------------
# please refer to services_unit.conf for ports
# either the -p flag to publish a range of ports or the -P flag to publish all
# of the exposed ports
# - 9001                supervisord
EXPOSE _===EXPOSE_PORTS===_

# -----------------------------------------------------------------------------
# Mount point from native host or other containers
# -----------------------------------------------------------------------------
VOLUME ["${ROOT_PATH}"]

# -----------------------------------------------------------------------------
# Entrypoint
# -----------------------------------------------------------------------------
ENTRYPOINT ["/etc/bootstrap.sh"]