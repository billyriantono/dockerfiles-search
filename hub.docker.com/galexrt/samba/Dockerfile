FROM debian:stretch

COPY testing.pref /etc/apt/preferences.d/testing.pref

RUN echo "deb http://http.us.debian.org/debian/ testing main non-free contrib" >> /etc/apt/sources.list \
 && export samba_version=4.9.1 \
 && export DEBIAN_FRONTEND=noninteractive \
 \
 && apt-get -q -y update \
 && apt-get -q -y upgrade \
 && apt-get -y install samba \
 && apt-get -y -t testing install samba-vfs-modules \
 && apt-get -q -y autoremove \
 && apt-get -q -y clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 \
 && touch /var/lib/samba/registry.tdb

VOLUME ["/shares"]

EXPOSE 139 445

COPY scripts /usr/local/bin/

HEALTHCHECK CMD ["docker-healthcheck.sh"]
ENTRYPOINT ["entrypoint.sh"]

CMD ["bash", "-c", "smbd -FS -d 2 < /dev/null"]
