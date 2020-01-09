FROM archimg/base-devel

RUN pacman --noconfirm -Sy
RUN pacman --noconfirm -S git biber
RUN pacman --noconfirm -S $(pacman -Sqs texlive-)

WORKDIR /tmp

RUN useradd -ms /bin/bash builduser
RUN echo "builduser ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER builduser

RUN git clone https://aur.archlinux.org/perl-term-shellui.git && \
    cd perl-term-shellui && \
    makepkg --noconfirm -si

RUN git clone https://aur.archlinux.org/texlive-localmanager-git.git && \
    cd texlive-localmanager-git && \
    makepkg --noconfirm -si

ENV PATH="/usr/bin/vendor_perl:${PATH}"

WORKDIR /build

ENTRYPOINT ./build.sh

