FROM samuelololol/docker-gentoo-websync
MAINTAINER aragaer <aragaer@gmail.com>
RUN rm /sbin/unix_chkpwd
RUN emerge sys-libs/db sys-libs/pam sys-apps/iproute2 dev-lang/perl \
    sys-libs/binutils-libs
    # helps to save time for building later image
RUN USE=cross-aarch64-unknown-linux-gnu/gcc emerge crossdev
RUN USE="${USE} crossdev" emerge distcc
RUN mkdir -p /usr/local/portage-crossdev/{profiles,metadata} && \
    echo 'crossdev' > /usr/local/portage-crossdev/profiles/repo_name && \
    echo 'masters = gentoo' > /usr/local/portage-crossdev/metadata/layout.conf && \
    chown -R portage:portage /usr/local/portage-crossdev
RUN ( \
    echo "[crossdev]" && \
    echo "location = /usr/local/portage-crossdev" && \
    echo "priority = 10" && \
    echo "masters = gentoo" && \
    echo "auto-sync = no" \
    ) > /etc/portage/repos.conf/crossdev.conf
RUN ( \
    echo "#!/bin/sh" && \
    echo "eval \"\`gcc-config -E\`\"" && \
    echo "exec distccd \"\$@\"" \
    ) > /usr/local/sbin/distccd-launcher && \
    chmod +x /usr/local/sbin/distccd-launcher
RUN emerge ccache && \
    echo 'FEATURES="ccache"' >> /etc/portage/make.conf && \
    echo 'CCACHE_SIZE="2G"' >> /etc/portage/make.conf && \
    echo 'CCACHE_MAXSIZE="2G"' >> /etc/portage/make.conf && \
    echo 'CCACHE_DIR="/var/tmp/portage/ccache"' >> /etc/portage/make.conf && \
    echo 'CCACHE_TEMPDIR="/var/tmp/portage/ccache"' >> /etc/portage/make.conf
RUN emerge -f binutils gcc linux-headers glibc
RUN crossdev -S -P "-v" -t armv7a-unknown-linux-gnueabihf
#RUN rm -r /usr/portage
ENTRYPOINT ["/usr/local/sbin/distccd-launcher"]
CMD ["--allow", "0.0.0.0/0", "--user", "distcc", "--log-level", "debug", "--log-stderr", "--no-detach"]
EXPOSE 3632
