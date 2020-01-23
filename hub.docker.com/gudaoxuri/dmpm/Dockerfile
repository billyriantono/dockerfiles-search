FROM base/archlinux

MAINTAINER Tao Guo <guotao945@gmail.com>

RUN pacman -Sy --noconfirm \
        base-devel \
        git \
        bash-completion \
        keychain \
        vim \
        tmux \
        tar \
        gtk-doc \
        yasm \
        dos2unix \
        pulseaudio \
        xterm \
        libxv \
        procps-ng \
        psmisc \
        gtk3 \
        intltool \
        json-glib \
        git-annex \
        gperf \
        gdb

RUN pacman -Scc --noconfirm

RUN sed -i -e 's/#en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen
RUN locale-gen
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

CMD /bin/bash
