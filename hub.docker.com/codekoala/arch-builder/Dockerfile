FROM codekoala/arch
MAINTAINER Josh VanderLinden <codekoala@gmail.com>

RUN useradd -MUu 1000 builduser
RUN pacman -Sy --noconfirm --needed \
        base-devel \
        rsync \
        python \
        python-pip \
        python-pytest \
        python-tox \
        python-wheel \
        spr
