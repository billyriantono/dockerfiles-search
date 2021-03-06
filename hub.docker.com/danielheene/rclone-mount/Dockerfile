FROM alpine:latest

# ENVIRONMENT VARIABLES
ENV CACHE_DIR       /cache
ENV CONFIG_DIR      /config
ENV CONFIG_FILE     rclone.conf
ENV LOG_DIR         /logs
ENV LOG_FILE        rclone.log
ENV LOG_LEVEL       NOTICE
ENV MOUNT_DIR       /mount
ENV MOUNT_NAME      mount
ENV MOUNT_PID_FILE  /var/run/rclone-mount.pid
ENV UID             1000
ENV GID             1000

# INSTALL RCLONE
RUN apk --no-cache add fuse ca-certificates \
    && cd /tmp \
    && wget -q http://downloads.rclone.org/rclone-current-linux-amd64.zip \
    && unzip -q rclone-current-linux-amd64.zip \
    && mv rclone-*-linux-amd64/rclone /bin/ \
    && chmod +x /bin/rclone \
    && rm -r rclone-*

# CREATE DIRECTORYS
RUN mkdir -p ${CACHE_DIR} ${CONFIG_DIR} ${LOG_DIR} ${MOUNT_DIR} 

# CREATE HEALTHCHECK
COPY scripts/check.sh /bin/rclone-check
RUN chmod +x /bin/rclone-check

# CREATE ENTRYPOINT
COPY scripts/mount.sh /bin/rclone-mount
RUN chmod +x /bin/rclone-mount

ENTRYPOINT [ "rclone-mount" ]
CMD [ ]
