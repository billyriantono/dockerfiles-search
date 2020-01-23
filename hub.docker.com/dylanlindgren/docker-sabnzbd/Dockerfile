FROM debian:sid

MAINTAINER “Dylan Lindgren” <dylan.lindgren@gmail.com>

WORKDIR /var/lib

# Install SABnzbd
RUN awk '{ print $0" contrib non-free" }' /etc/apt/sources.list > /etc/apt/sources.tmp && \
    mv /etc/apt/sources.tmp /etc/apt/sources.list && \
    apt-get update -y && \
    apt-get install -y \
    python2.7 \
    sabnzbdplus \
    sabnzbdplus-theme-mobile \
    unrar && \
    rm -rf /var/lib/apt/lists/*

# Create SickBeard user and set permissions
RUN useradd -c "SABnzbd User" sabnzbd && \
    mkdir -p /data/sabnzbd && \
    mkdir -p /data/nzb && \
    chown -R sabnzbd:sabnzbd /data/sabnzbd /data/nzb
VOLUME ["/data/sabnzbd"]
VOLUME ["/data/nzb"]

EXPOSE 8080

ENTRYPOINT ["/usr/bin/sabnzbdplus", "--config-file", "/data/sabnzbd/config.ini", "--server",":8080"]