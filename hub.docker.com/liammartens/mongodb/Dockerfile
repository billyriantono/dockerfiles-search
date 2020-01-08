ARG USER=mongo
FROM liammartens/alpine
LABEL maintainer="Liam Martens <hi@liammartens.com>"

# @user Use root user for install
USER root

# @run Install packages
RUN apk add mongodb pwgen

# @run make directory
RUN mkdir -p /data /etc/mongod

# @copy Copy conf
COPY conf/* /etc/mongod/

# @run chown for user
RUN chown -R ${USER}:${USER} /data /etc/mongod

# @copy Copy additional run files
COPY .docker ${DOCKER_DIR}

# @run Make the file(s) executable
RUN chmod -R +x ${DOCKER_DIR}

# @user Switch back to non-root user
USER ${USER}

# @healthcheck
HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=2 CMD mongo --port "${MONGODB_PORT}" --eval "quit()" || exit 1

CMD [ "-c", "mongod --auth -f /etc/mongod/mongod.conf --logpath /proc/self/fd/2"]