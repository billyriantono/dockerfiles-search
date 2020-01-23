FROM debian:sid-slim
# hadolint ignore=DL3008
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        ca-certificates \
        gettext-base \
        ldap-account-manager \
        libcap2-bin \
        patch \
        wget \
    && \
    setcap CAP_NET_BIND_SERVICE=+ep /usr/sbin/apache2 && \
    install -d -m 750 -o root -g www-data /var/log/apache2 && \
    install -d -m 755 -o www-data -g root /run/apache2 && \
    a2enmod status && \
    ln -sf /dev/stdout /var/log/apache2/access.log && \
    ln -sf /dev/stderr /var/log/apache2/error.log && \
    ln -sf /dev/stdout /var/log/apache2/lam.log && \
    ln -sf /dev/stdout /var/log/apache2/other_vhosts_access.log && \
    rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/* /var/cache/apt/archives/*
ENV APACHE_RUN_DIR=/run/apache2 \
    APACHE_LOG_DIR=/var/log/apache2 \
    APACHE_RUN_USER=www-data \
    APACHE_RUN_GROUP=www-data \
    APACHE_PID_FILE=/run/apache2/apache2.pid
COPY --chown=root:root patch.diff /root/
COPY --chown=root:root entrypoint /usr/local/bin/
COPY --chown=root:root lam-setpass /usr/local/bin/
RUN patch --strip 0 --verbose --directory / --input /root/patch.diff && \
    apache2 -t
ENV LDAP_URI=ldapi:/// \
    LAM_PASSWORD=lam
EXPOSE 80
USER "www-data"
WORKDIR /var/www
ENTRYPOINT [ "entrypoint" ]
CMD [ "apache2", "-DFOREGROUND" ]
HEALTHCHECK CMD wget --spider --quiet http://localhost/lam/ --user-agent 'Healthcheck' || exit 1
