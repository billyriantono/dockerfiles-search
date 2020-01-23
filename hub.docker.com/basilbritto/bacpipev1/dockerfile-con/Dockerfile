FROM resin/amd64-debian:stretch

ENV DEBIAN_FRONTEND noninteractive
ENV container docker
ENV init /lib/systemd/systemd
ENV LC_ALL C

RUN apt-get update && apt-get -y install procps less systemd ; \
    [ -e /lib/systemd/system/sysinit.target.wants/ ] && \
      find /lib/systemd/system/sysinit.target.wants/ ! -name 'systemd-tmpfiles-setup.service' -type f -o -type l -exec rm -f {} \; || true; \
    [ -e /lib/systemd/system/local-fs.target.wants/ ] && \
      find /lib/systemd/system/multi-user.target.wants/ -type f -o -type l -exec rm -f {} \; || true; \
    find /etc/systemd/system/*.wants/ -type f -o -type l -exec rm -f {} \; || true; \
    [ -e /lib/systemd/system/local-fs.target.wants/ ] && \
      find /lib/systemd/system/local-fs.target.wants/ -type f -o -type l -exec rm -f {} \; || true; \
    [ -e /lib/systemd/system/sockets.target.wants/ ] && \
      find /lib/systemd/system/sockets.target.wants/ -iname '*udev*' -o -iname '*initctl*' -exec rm -f {} \; || true; \
    [ -e /usr/lib/tmpfiles.d/systemd-nologin.conf ] && rm -f /usr/lib/tmpfiles.d/systemd-nologin.conf || true

RUN sed -i'' -e 's/.*SystemMaxUse=.*/SystemMaxUse=500M/' /etc/systemd/journald.conf ; \
    mkdir -p /usr/local/lib/systemd/system

ADD docker/systemd/minera.service /usr/local/lib/systemd/system/

RUN ln -s /usr/local/lib/systemd/system/minera.service /etc/systemd/system/multi-user.target.wants/minera.service

RUN printf '# Do not install recommended and suggested packages by default\n\
APT::Install-Recommends "0";\n\
APT::Install-Suggests "0";\n' > /etc/apt/apt.conf.d/docker-skip-recommends-suggests

# build-essential libblkmaker-0.1-dev libtool libcurl4-openssl-dev libjansson-dev libudev-dev libncurses5-dev autoconf automake postfix redis-server git screen php7.0-cli php7.0-curl php7.0-fpm php7.0-readline php7.0-json wicd-curses uthash-dev libmicrohttpd-dev libevent-dev libusb-dev libusb-dev shellinabox supervisor lighttpd libssl-dev
RUN apt-get update && apt-get -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" install -y \
       build-essential libtool libcurl4-openssl-dev libjansson-dev libudev-dev libncurses5-dev \
       pkg-config file libbase58-dev \
       autoconf automake postfix redis-server git screen \
       php7.0-cli php7.0-curl php7.0-fpm php7.0-readline php7.0-json \
       wicd-curses uthash-dev libmicrohttpd-dev libevent-dev shellinabox supervisor lighttpd libssl-dev && \
       apt-get -y clean && \
       rm -rf /var/lib/apt/lists/*


RUN mkdir -p /var/www/minera
ADD . /var/www/minera
RUN  cd /var/www/minera/minera-bin/src/libblkmaker/ && ./configure && make || true; \


RUN [ -e /etc/systemd/system/default.target ] && rm /etc/systemd/system/default.target || true ; \
    ln -s /usr/lib/systemd/system/multi-user.target /etc/systemd/system/default.target

#RUN systemctl set-default multi-user.target


VOLUME [ "/sys/fs/cgroup" ]
# Workaround hack for missing /sys/fs/cgroup (This works on Docker Machine, but YMMV)
CMD ["/bin/bash", "-c", "mount -oremount,rw /sys/fs/cgroup; mkdir /sys/fs/cgroup/systemd; mount -oremount,ro /sys/fs/cgroup; exec /lib/systemd/systemd"]

# TODO: If possible, somehow cleanup above hack, & replace with either:
#ENTRYPOINT ["/lib/systemd/systemd"]
#CMD ["/usr/sbin/init"]
