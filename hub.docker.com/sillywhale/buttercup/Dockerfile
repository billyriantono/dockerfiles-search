FROM debian:stretch

LABEL maintainer="SillyWhale <contact@sillywhale.wtf>"

### Install base package
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    libnss3 libasound2 libgconf-2-4 libxtst6 libx11-xcb1 \
    ca-certificates wget libxss1 libgtk-3-0 curl && \
    update-ca-certificates && \
    rm -rf /var/lib/apt/lists/*


### Install de Postman
RUN mkdir -p /opt/buttercup && \
    cd /tmp/ && \
    wget -q -O /tmp/buttercup.AppImage https://github.com/buttercup/buttercup-desktop/releases/download/v1.14.0/buttercup-desktop-1.14.0-x86_64.AppImage && \
    chmod +x /tmp/buttercup.AppImage && \
    /tmp/buttercup.AppImage --appimage-extract && \
    mv squashfs-root/* /opt/buttercup/ && \
    chmod 777 -R /opt/buttercup && \
		rm -rf /tmp/buttercup.AppImage /tmp/squashfs-root && \
    curl -s https://api.github.com/repos/buttercup/buttercup-desktop/releases/latest | grep tag_name | cut -d '"' -f 4 > /opt/buttercup/version

WORKDIR /opt/buttercup

ENTRYPOINT ["/opt/buttercup/buttercup-desktop"]
