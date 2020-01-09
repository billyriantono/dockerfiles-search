FROM debian:buster-slim
# hadolint ignore=DL3008,DL3015
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        apache2 \
        cgit \
        groff-base \
        libcap2-bin \
        patch \
        python3-docutils \
        python3-markdown \
        python3-pygments \
    && \
    setcap CAP_NET_BIND_SERVICE=+ep /usr/sbin/apache2 && \
    a2enmod cgid && \
    a2enconf cgit && \
    a2enmod status && \
    install -d -o www-data -g www-data -m 755 /var/cache/cgit && \
    install -d -o www-data -g www-data -m 755 /run/apache2 && \
    install -d -o www-data -g www-data -m 755 /var/log/apache2 && \
    ln -sf /dev/stdout /var/log/apache2/access.log && \
    ln -sf /dev/stderr /var/log/apache2/error.log && \
    ln -sf /dev/stdout /var/log/apache2/other_vhosts_access.log && \
    rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/* /var/cache/apt/archives/*
COPY --chown=root:root patch.diff /root/
COPY --chown=root:root cgitrc /etc/
ENV APACHE_RUN_DIR=/run/apache2 \
    APACHE_LOG_DIR=/var/log/apache2 \
    APACHE_RUN_USER=www-data \
    APACHE_RUN_GROUP=www-data \
    APACHE_PID_FILE=/run/apache2/apache2.pid
RUN patch --strip 0 --verbose --directory /etc/apache2 --input /root/patch.diff && \
    apache2 -t
EXPOSE 8080
CMD [ "apache2", "-DFOREGROUND" ]
VOLUME ["/srv/git"]
USER "www-data"
WORKDIR /var/www
HEALTHCHECK CMD wget --spider --quiet http://localhost:8080/cgit/ --user-agent 'Healthcheck' || exit 1
