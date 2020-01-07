FROM hongkongkiwi/alpine-node-docker:latest

MAINTAINER Andy Savage <andy@savage.hk>

LABEL org.label-schema.name="docker-node-docker-supercronic" \
      org.label-schema.description="Useful base docker image which includes a base system with Node.js, Docker & Supercronic" \
      org.label-schema.vcs-url="https://github.com/hongkongkiwi/docker-alpine-node-supercronic" \
      org.label-schema.license="MIT"

ARG OS="linux"
ARG ARCH="amd64"

ARG SUPERCRONIC_VER="v0.1.5"
ARG SUPERCRONIC_URL="https://github.com/aptible/supercronic/releases/download/${SUPERCRONIC_VER}/supercronic-${OS}-${ARCH}"
ARG SUPERCRONIC="supercronic-${OS}-${ARCH}"
ARG SUPERCRONIC_SHA1SUM="9aeb41e00cc7b71d30d33c57a2333f2c2581a201"
ENV SUPERCRONIC_INSTALL_PATH="/usr/local/bin"

ENV CRONTAB_FILE="/etc/crontab"

COPY supercronic-start.sh /usr/local/bin/supercronic-start.sh

RUN echo "Installing Packages" \
 && apk update \
 && apk add --no-cache curl ca-certificates openssl \
 && echo "Downloading Supercronic" \
 && curl -fsSLO "$SUPERCRONIC_URL" \
 && echo "Checking Supercronic Downloaded Checksums" \
 && echo "${SUPERCRONIC_SHA1SUM}  ${SUPERCRONIC}" | sha1sum -c - \
 && echo "Installing Supercronic" \
 && chmod +x "$SUPERCRONIC" "/usr/local/bin/supercronic-start.sh" \
 && mv "$SUPERCRONIC" "/usr/local/bin/${SUPERCRONIC}" \
 && ln -s "/usr/local/bin/${SUPERCRONIC}" "${SUPERCRONIC_INSTALL_PATH}/supercronic" \
 && touch "${CRONTAB_FILE}" \
 && echo "Cleaning Up" \
 && apk del --purge curl ca-certificates openssl \
 && rm -rf /var/cache/apk/*

ENTRYPOINT ["/usr/local/bin/supercronic-start.sh"]
CMD ["/usr/local/bin/supercronic-start.sh"]
