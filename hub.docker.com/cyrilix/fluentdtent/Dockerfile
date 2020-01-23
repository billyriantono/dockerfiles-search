FROM centos:7
LABEL maintainer="Abdelkarim MALI <a.mali@cyfratech.net>"

ARG VERSION=v1.3.0

RUN yum -y update && \
    yum -y install wget unzip && \
    yum clean all && \
    wget -O /tmp/sia.zip https://github.com/NebulousLabs/Sia/releases/download/$VERSION/Sia-$VERSION-linux-amd64.zip && \
    unzip -d /tmp /tmp/sia.zip && \
    mv /tmp/Sia-$VERSION-linux-amd64/siac /usr/local/bin/ && \
    mv /tmp/Sia-$VERSION-linux-amd64/siad /usr/local/bin/ && \
    rm -rf /tmp/*

VOLUME ["/siadata"]

WORKDIR /siadata

EXPOSE 9980 9981 9982

ENTRYPOINT ["/usr/local/bin/siad"]
