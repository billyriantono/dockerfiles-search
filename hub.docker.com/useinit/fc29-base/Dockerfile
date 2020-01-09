FROM registry.fedoraproject.org/fedora:29 AS builder

RUN curl -L -o /etc/yum.repos.d/_copr_mskarbek-dinit.repo https://copr.fedorainfracloud.org/coprs/mskarbek/dinit/repo/fedora-29/mskarbek-dinit-fedora-29.repo \
  && dnf clean all \
  && dnf -y update rpm* dnf*

RUN mkdir -p /srv/rootfs/etc/rpm \
 && echo "%_install_langs C:en:en_US:en_US.UTF-8" > /srv/rootfs/etc/rpm/macros.image-language-conf \
 && dnf -y --installroot=/srv/rootfs --nodocs --releasever=29 \
    --disablerepo='*' --enablerepo=fedora --enablerepo=updates \
    --enablerepo=mskarbek-dinit --setopt=install_weak_deps=False \
      install \
        coreutils-single \
        cracklib-dicts \
        dbus-broker \
        dinit \
        fedora-release \
        glibc-common \
        glibc-langpack-en \
        glibc-minimal-langpack \
        langpacks-en \
        microdnf \
        passwd \
        rpm \
        systemd \
        vim-minimal \
 && dnf --installroot=/srv/rootfs clean all

FROM scratch

COPY --from=builder /srv/rootfs .

RUN systemctl enable dbus-broker \
 && useradd -m -s /bin/bash core
