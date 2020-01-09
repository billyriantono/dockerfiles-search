FROM php:7.1-apache-stretch
LABEL maintainer="Christian-Maximilian Steier"

ARG VERSION=19.04
ARG RELEASE=.0
ARG minimal_apt_get_install='apt-get install -y --no-install-recommends'
ENV DEBIAN_FRONTEND=noninteractive \
DEBCONF_NONINTERACTIVE_SEEN=true

# System
ADD scripts /scripts
RUN \
    # Cleanup Based on https://gist.github.com/jumanjiman/f9d3db977846c163df12 \
    export sysdirs="/bin /etc /lib /sbin /usr" && \
    echo -e "[i] Remove crufty...\n   /etc/shadow-\n   /etc/passwd-\n   /etc/group-" && \
    find $sysdirs -xdev -type f -regex '.*-$' -exec rm -f {} + && \
    echo "[i] Ensure system dirs are owned by root and not writable by anybody else." && \
    find $sysdirs -xdev -type d -exec chown root:root {} \; -exec chmod 0755 {} \; && \
    echo "[i] Set wright permissions for /tmp and /var/tmp." && \
    chmod a=rwx,o+t /tmp /var/tmp && \
    echo "[i] Remove all suid files." && \
    find $sysdirs -xdev -type f -a -perm -4000 -delete && \
    echo "[i] Remove init scripts" && \
    rm -fr /etc/init.d /lib/rc /etc/conf.d /etc/inittab /etc/runlevels /etc/rc.conf && \
    echo "[i] Remove kernel tunables" && \
    rm -fr /etc/sysctl* /etc/modprobe.d /etc/modules /etc/mdev.conf /etc/acpi && \
    echo "[i] Remove broken symlinks." && \
    find $sysdirs -xdev -type l -exec test ! -e {} \; -delete && \
    \
    /scripts/prepare.sh && \
    /scripts/system_services.sh && \
    /scripts/utilities.sh && \
    /scripts/php-extensions.sh && \
    # Composer \
    echo "\n[i] Install Composer\n" && \
    curl -sS https://getcomposer.org/installer | php && \
    chmod +x ./composer.phar && \
    mv ./composer.phar /usr/local/bin/composer

# Copy local files
COPY root/ /

ENTRYPOINT ["/init"]
