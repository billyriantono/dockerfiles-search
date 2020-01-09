FROM debian:stable-slim
MAINTAINER Ryan Lieu <github-benzBrake@woai.ru>
RUN apt-get update && \
    apt-get -y install curl && \
    CT_VER=$(curl -s "https://github.com/jpillora/cloud-torrent/releases/latest" | perl -e 'while($_=<>){ /\/tag\/(.*)\">redirected/; print $1;}') && \
    curl -L "https://github.com/jpillora/cloud-torrent/releases/download/${CT_VER}/cloud-torrent_linux_386.gz" -o cloud-torrent.gz && \
    gzip -d cloud-torrent.gz && \
    mv cloud-torrent /usr/bin/cloud-torrent && \
    chmod +x /usr/bin/cloud-torrent
ENTRYPOINT /usr/bin/cloud-torrent