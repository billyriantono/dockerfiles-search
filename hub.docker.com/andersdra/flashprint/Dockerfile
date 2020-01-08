# docker-flashprint
# Incompatible Qt version on Buster
from debian:stretch-20190506-slim

LABEL maintainer="Anders Draagen <andersdra@gmail.com>"

ARG FLASHPRINT_RAR_URL='https://www.flashforge.com/wp-content/uploads/2017/04/flashprint_3.24.0_Linux64.rar'

ARG C_USER=flashprint
ARG C_UID=1000
ARG C_GUID=1000

ADD ${FLASHPRINT_RAR_URL} /tmp

RUN apt-get update \
    && apt-get install --yes --no-install-recommends \
    libglu1-mesa \
    libgl1-mesa-dri \
    libudev-dev \
    libqt5gui5 \
    libqt5core5a \ 
    libqt5opengl5 \
    libqt5network5 \
    libqt5xml5 \
    unrar-free \
    && unrar -x /tmp/flashprint_*_Linux64.rar /tmp \
    && dpkg -i /tmp/flashprint_*_amd64.deb \
    && apt-get --fix-broken --yes install \
    && groupadd \
    --system ${C_USER} \
    --gid ${C_GUID} \
    && useradd \
    --no-log-init --uid ${C_UID} \
    --system --gid ${C_USER} \
    --create-home --home-dir /${C_USER} \
    --shell /sbin/nologin \
    --comment \"${C_USER}\" ${C_USER} \
    && chmod 771 /${C_USER} \
    && rm -rf /tmp/* && chown -R ${C_USER}:${C_USER} /${C_USER} \
    && apt-get -qq purge --auto-remove --yes --allow-remove-essential \
    systemd \
    systemd-sysv \
    && apt-get -qq remove --yes unrar-free \
    && apt-get -qq clean autoclean \
    && apt-get -qq autoremove --yes \
    && rm -rf /usr/share/man/* \
    && rm -rf /tmp/* \
    && rm -rf /var/log/* \
    && rm -rf /var/lib/{apt,dpkg,cache,log}/

ENV USER=${C_USER}
ENV HOME=/${C_USER}

USER ${C_USER}
WORKDIR /${C_USER}

CMD ["/usr/share/FlashPrint/FlashPrint"]
