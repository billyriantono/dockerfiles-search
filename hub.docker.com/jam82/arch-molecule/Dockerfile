FROM archlinux/base
LABEL maintainer="jam82"

ENV container docker

RUN pacman -Syu --noconfirm \
    && pacman --sync --noconfirm --refresh \
    awk \
    bash \
    grep \
    procps-ng \
    python \
    python-pip \
    sed \
    sudo \
    systemd-sysvcompat \
    vim \
    && pacman -Scc --noconfirm \
    && (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done) \
    && rm -f /lib/systemd/system/multi-user.target.wants/*;\
    rm -f /etc/systemd/system/*.wants/*;\
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*; \
    rm -f /lib/systemd/system/anaconda.target.wants/*; \
    pip install ansible; \
    mkdir -p /etc/ansible; \
    echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts
    
VOLUME ["/sys/fs/cgroup"]

CMD ["/usr/lib/systemd/systemd"]
