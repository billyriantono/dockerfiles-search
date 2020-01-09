FROM bitnami/minideb-extras-base:stretch

RUN install_packages gnupg
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && install_packages nodejs
RUN npm install ghost-cli@latest -g
RUN install_packages mariadb-client

ENV GHOST_VERSION="2.16.2" \
    DATABASE_HOST="mariadb" \
    DATABASE_PORT_NUMBER="3306" \
    DATABASE_USER="ghost" \
    DATABASE_NAME="ghost" \
    DATABASE_PASSWORD="" \
    GHOST_HOST="localhost" \
    GHOST_PORT_NUMBER="80" \
    GHOST_USER="user" \
    GHOST_EMAIL="user@example.com" \
    GHOST_BLOG_TITLE="User's Blog!" \
    GHOST_PASSWORD="MyP4ssW0rd"

COPY rootfs /

RUN /prepare.sh

WORKDIR /opt/ghost
VOLUME /data/ghost
EXPOSE 3000

USER nonroot

ENTRYPOINT ["/entrypoint.sh"]
CMD ["/run.sh"]
