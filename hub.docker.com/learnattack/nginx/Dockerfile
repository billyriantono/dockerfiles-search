FROM bitnami/nginx:1.16.1
LABEL maintainer="Learnattack <it@learnattack.de>"

# Run privileged commands
USER 0

COPY nginx/rootfs /
# Build brotli for NGINX version
RUN install_packages \
    brotli \
    build-essential \
    gcc \
    git \
    gosu \
    libpcre3-dev \
    libssl-dev \
    zlib1g-dev \
  && /libbrotli.sh "1.16.1" \
  && apt-get purge -y \
    build-essential \
    gcc \
    git \
    libpcre3-dev \
    libssl-dev \
    zlib1g-dev \
  && apt-get -y clean \
  && apt-get -y autoclean \
  && apt-get -y autoremove \
  && rm -rf /var/lib/apt/lists/* && rm -rf /var/lib/cache/* && rm -rf /var/lib/log/* && rm -rf /tmp/*

# Set user back to default
USER 1001
