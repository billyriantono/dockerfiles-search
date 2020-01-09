FROM archlinux/base:latest

LABEL maintainer="André Gomes<bmg.andre@gmail.com>"
LABEL version="0.2.0"

RUN pacman -Suuy --noconfirm
RUN pacman -S --noconfirm \
        grep \
        which \
        git \
        make \
        texlive-most \
        po4a
