FROM base/archlinux
MAINTAINER Mikhail Belyaev

RUN pacman --noconfirm -Syy

RUN pacman --noconfirm -Sc && \
    pacman --noconfirm -S archlinux-keyring

RUN pacman --noconfirm -S pacman && pacman-db-upgrade

# upgrade system and install dependencies
RUN pacman --noconfirm -Syyu && \
    pacman --noconfirm -S base-devel yajl sudo rsync git

# regenerate locales
RUN echo "en_US.UTF-8 UTF-8" >/etc/locale.gen && locale-gen

# add yaourt user and group
RUN groupadd -r yaourt && \
    useradd -r -g yaourt yaourt
RUN mkdir /tmp/yaourt && \
    chown -R yaourt:yaourt /tmp/yaourt

# configure sudo for pacman
ADD container_files/yaourt_sudo /etc/sudoers.d/yaourt

# install package-query
USER yaourt
RUN cd /tmp/yaourt && \
    git clone https://aur.archlinux.org/package-query.git /tmp/yaourt/package-query && \
    cd /tmp/yaourt/package-query && \
    makepkg --noconfirm
USER root
RUN cd /tmp/yaourt/package-query && \
    pacman --noconfirm -U *.tar.xz

# install yaourt
USER yaourt
RUN cd /tmp/yaourt && \
    git clone https://aur.archlinux.org/yaourt.git /tmp/yaourt/yaourt && \
	cd /tmp/yaourt/yaourt && \
	makepkg --noconfirm
USER root
RUN cd /tmp/yaourt/yaourt && \
	pacman --noconfirm -U *.pkg.tar.xz
