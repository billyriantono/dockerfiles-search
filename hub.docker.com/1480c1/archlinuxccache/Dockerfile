FROM archlinux/base:latest
LABEL maintainer="Christopher Degawa <ccom@randomderp.com>" \
    name="ccacheBuilds" \
    description="ccache container for ci" \
    vcs-url="https://github.com/1480c1/ccacheBuilds" \
    License="MIT License" \
    version="0.0.1"

RUN pacman -Sy --ask=20 --noconfirm --noprogressbar --needed \
    ccache \
    clang \
    llvm \
    gcc && \
    ln -s /usr/sbin/ccache /usr/local/bin/clang && \
    ln -s /usr/sbin/ccache /usr/local/bin/clang++ && \
    ln -s /usr/sbin/ccache /usr/local/bin/gcc && \
    ln -s /usr/sbin/ccache /usr/local/bin/g++ && \
    ln -s /usr/sbin/ccache /usr/local/bin/cc && \
    ln -s /usr/sbin/ccache /usr/local/bin/c++ && \
    mkdir /root/.ccache/ && \
    ln -s /root/.ccache/ /ccache && \
    pacman -Scc --ask=20 --noconfirm

VOLUME [ "/ccache" ]
