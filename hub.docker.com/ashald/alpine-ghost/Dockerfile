FROM node:argon-alpine

ENV GHOST_VERSION 0.11.7
ENV GHOST_SOURCE /usr/src/ghost
ENV GHOST_CONTENT /var/lib/ghost
ENV GHOST_USER ghost
ENV GHOST_GROUP ghost

RUN addgroup $GHOST_GROUP && \
    adduser -SHG $GHOST_GROUP $GHOST_USER

WORKDIR $GHOST_SOURCE

RUN apk --no-cache add tar tini su-exec \
    && apk --no-cache add --virtual devs gcc make python wget unzip ca-certificates \
    && wget -O ghost.zip https://github.com/TryGhost/Ghost/releases/download/${GHOST_VERSION}/Ghost-${GHOST_VERSION}.zip \
    && unzip ghost.zip \
    && npm install --production \
    && rm ghost.zip \
    && apk del devs \
    && npm cache clean \
    && rm -rf /tmp/npm*

ENV NODE_ENV production

COPY ./entrypoint.sh /
RUN chmod +x /entrypoint.sh

EXPOSE 2368

ENTRYPOINT ["/entrypoint.sh"]

CMD ["/sbin/tini", "--", "node", "index"]
