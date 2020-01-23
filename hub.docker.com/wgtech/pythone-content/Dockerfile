FROM debian:stretch

# Update system and install required packages
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -qq \
    && apt-get install -y \
        git cpanminus procps build-essential \
        libjson-webtoken-perl \
        libauthen-ntlm-perl \
        libcgi-pm-perl \
        libcrypt-openssl-rsa-perl \
        libdata-uniqid-perl \
        libfile-copy-recursive-perl \
        libio-socket-ssl-perl \
        libio-tee-perl \
        libhtml-parser-perl \
        libjson-webtoken-perl \
        libmail-imapclient-perl \
        libparse-recdescent-perl \
        libmodule-scandeps-perl \
        libreadonly-perl \
        libsys-meminfo-perl \
        libterm-readkey-perl \
        libtest-mockobject-perl \
        libtest-pod-perl \
        libunicode-string-perl \
        liburi-perl  \
        libwww-perl \
        libclass-load-perl \
        libpar-packer-perl \
        libio-socket-inet6-perl \
        libdist-checkconflicts-perl \
        libmodule-implementation-perl \
        libpackage-stash-perl \
        libpackage-stash-xs-perl \
        libtest-fatal-perl \ 
        libtest-mock-guard-perl \
        libtest-requires-perl \
        libtry-tiny-perl \
    && apt-get clean autoclean \
    && apt-get autoremove --yes \
    && rm -rf /var/lib/{apt,dpkg,cache,log}/

ENV VERSION 1.836

RUN \
    git clone  --depth 1 --branch imapsync-${VERSION} git://github.com/imapsync/imapsync.git && \
	make -C imapsync/ install && \
    rm -rf imapsync

ENTRYPOINT ["/usr/bin/imapsync"]