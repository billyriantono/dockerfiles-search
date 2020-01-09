FROM centos:7
LABEL maintainer="Bryan Hundven <bryanhundven@gmail.com>"

ENV SHELL /bin/bash

RUN set -eux && \
    rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 && \
    yum install -y epel-release ca-certificates && \
    rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7 && \
    update-ca-trust force-enable && \
    yum install -y \
        device-mapper-persistent-data \
        lvm2 \
        yum-utils && \
    yum install -y https://centos7.iuscommunity.org/ius-release.rpm && \
    rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-IUS-7 && \
    yum-config-manager --add-repo \
        https://download.docker.com/linux/centos/docker-ce.repo && \
    rpm --import https://download.docker.com/linux/centos/gpg && \
    yum install -y \
        btrfs-progs \
        containerd.io \
        docker-ce \
        docker-ce-cli \
        e2fsprogs \
        e2fsprogs-extra \
        gcc \
        git2u \
        iptables \
        jq \
        libc-dev \
        make \
        openssh-client \
        openssl \
        pigz \
        shadow-uidmap \
        wget \
        which \
        xfsprogs \
        xz

RUN set -eux && \
    groupadd -r dockremap && \
    useradd -r -g dockremap dockremap && \
    echo 'dockremap:165536:65536' >> /etc/subuid && \
    echo 'dockremap:165536:65536' >> /etc/subgid

# https://github.com/docker/docker/tree/master/hack/dind
ENV DIND_COMMIT 37498f009d8bf25fbb6199e8ccd34bed84f2874b

RUN set -eux && \
    wget -O /usr/local/bin/dind "https://raw.githubusercontent.com/docker/docker/${DIND_COMMIT}/hack/dind" && \
    chmod +x /usr/local/bin/dind

COPY dockerd-entrypoint.sh /usr/local/bin/

VOLUME /var/lib/docker
EXPOSE 2375 2376

ENTRYPOINT ["dockerd-entrypoint.sh"]
CMD []
