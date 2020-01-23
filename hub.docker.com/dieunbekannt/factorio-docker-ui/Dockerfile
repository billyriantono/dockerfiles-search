FROM frolvlad/alpine-glibc:alpine-3.9

LABEL maintainer="https://github.com/factoriotools/factorio-docker"

ARG USER=factorio
ARG GROUP=factorio
ARG PUID=845
ARG PGID=845

ENV PORT=34197 \
    RCON_PORT=27015 \
    VERSION=0.17.78 \
    SHA1=84bc37a586571b4358559dff5f8d95ef7305f7f7 \
    SAVES=/factorio/saves \
    CONFIG=/factorio/config \
    MODS=/factorio/mods \
    SCENARIOS=/factorio/scenarios \
    DATA=/factorio \
    MANAGER=/factoriomanager \
    SCRIPTOUTPUT=/factorio/script-output \
    PUID="$PUID" \
    PGID="$PGID" \
    MANAGER_VERSION=0.8.1 \
    ADMIN_PASSWORD=factorio

RUN set -ox pipefail \
    && archive="/tmp/factorio_headless_x64_$VERSION.tar.xz" \
    && mkdir -p /opt /factorio \
    && apk add --update --no-cache --no-progress bash binutils curl file gettext jq libintl pwgen shadow su-exec \
    && curl -sSL "https://www.factorio.com/get-download/$VERSION/headless/linux64" -o "$archive" \
    && echo "$SHA1  $archive" | sha1sum -c \
    || (sha1sum "$archive" && file "$archive" && exit 1) \
    && tar xf "$archive" --directory /opt \
    && chmod ugo=rwx /opt/factorio \
    && rm "$archive" \
    && ln -s "$SAVES" /opt/factorio/saves \
    && ln -s "$MODS" /opt/factorio/mods \
    && ln -s "$SCENARIOS" /opt/factorio/scenarios \
    && ln -s "$SCRIPTOUTPUT" /opt/factorio/script-output \
    && ln -s "$DATA" /opt/factorio \
    && ln -s /opt/factorio-server-manager "$MANAGER"  \
    && addgroup -g "$PGID" -S "$GROUP" \
    && adduser -u "$PUID" -G "$GROUP" -s /bin/sh -SDH "$USER" \
    && chown -R "$USER":"$GROUP" /opt/factorio /factorio
RUN apk add --no-cache curl tar unzip nginx openssl xz
WORKDIR /opt/
RUN curl -s -L -S -k https://github.com/mroote/factorio-server-manager/releases/download/$MANAGER_VERSION/factorio-server-manager-linux.zip --cacert /opt/github.pem -o /tmp/factorio-server-manager-linux_$MANAGER_VERSION.zip && \
    unzip -qq /tmp/factorio-server-manager-linux_$MANAGER_VERSION.zip && \
    rm /tmp/factorio-server-manager-linux_$MANAGER_VERSION.zip && \
    mkdir -p /run/nginx && \
    chown nginx:root /var/lib/nginx
COPY "init.sh" "/opt/init.sh"
COPY "nginx.conf" "/etc/nginx/nginx.conf"

VOLUME /factorio

EXPOSE $PORT/udp $RCON_PORT/tcp 80/tcp 443/tcp

COPY files/ /

ENTRYPOINT ["/docker-entrypoint.sh"]
