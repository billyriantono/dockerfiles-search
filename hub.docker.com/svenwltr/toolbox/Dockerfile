FROM fedora:25

RUN set -ex \
 && dnf -y install \
        bind-utils \
        mtr \
        nmap-ncat \
        procps-ng \
        screen \
        tar \
 && dnf clean all \
 && rm -rf /var/cache/yum/* \
 && cd /usr/local/bin \
 && curl -O https://storage.googleapis.com/kubernetes-release/release/v1.5.2/bin/linux/amd64/kubectl \
 && chmod +x kubectl
