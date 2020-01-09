FROM alpine:latest

LABEL maintainer="Frederic S." mail="nomuas@gmail.com"
LABEL description="Minimum container for rclone"
LABEL version="1.0"

# Global environment settings
ENV RCLONE_VERSION="v1.49.2" \
    PLATFORM_ARCH="amd64"

RUN \
# Install packages and update system
  apk update && \
  apk upgrade && \
  apk add --no-cache ca-certificates bash wget curl unzip fuse && \
  sed -i 's/^#user_allow_other/user_allow_other/' /etc/fuse.conf && \
# Install rclone
  cd /tmp && \
  wget -q https://downloads.rclone.org/${RCLONE_VERSION}/rclone-${RCLONE_VERSION}-linux-${PLATFORM_ARCH}.zip && \
  unzip /tmp/rclone-${RCLONE_VERSION}-linux-${PLATFORM_ARCH}.zip && \
  mv /tmp/rclone-*-linux-${PLATFORM_ARCH}/rclone /usr/bin && \
# Clean system
  rm -rf /tmp/* /var/tmp/* /var/cache/apk/* && \
# Add user & group
  addgroup rclone && \
  adduser -s /bin/bash -G rclone -D rclone

COPY root/ /

USER rclone
WORKDIR /home/rclone

ENTRYPOINT ["/entrypoint.sh"]
