FROM kalilinux/kali-linux-docker

RUN set -x \
    && apt-get -yqq update \
    && apt-get -yqq upgrade \
    && apt-get -yqq dist-upgrade \
    && apt-get -yqq install kali-linux-full \
    && apt-get -yqq autoremove \
    && apt-get -yqq clean \
    && rm -rf /var/lib/apt/lists* /var/tmp/* /tmp/*
CMD ["bash"]

