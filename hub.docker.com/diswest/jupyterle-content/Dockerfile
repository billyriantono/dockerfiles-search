FROM archlinux/base

RUN pacman --quiet --noconfirm -Sy
RUN pacman --quiet --noconfirm -S archlinux-keyring
RUN pacman --quiet --noconfirm -Syu
RUN pacman-db-upgrade
RUN pacman --quiet --noconfirm -S \
    base-devel \
	git \
	patchutils \
	wget \
	python \
	perl-proc-processtable

RUN if [ ! -z "$(pacman -Qtdq)" ]; then \
        pacman --noconfirm -Rns $(pacman -Qtdq); \
        fi
RUN pacman -Scc --noconfirm

RUN usermod --home /tmp/nobody --shell /bin/sh nobody

ADD toolchain/apollolake-gcc493_glibc220_linaro_x86_64-GPL.txz /usr/local
ADD toolchain/ds.apollolake-6.2.dev.txz /

VOLUME /dsm-media_build

WORKDIR /dsm-media_build

CMD /bin/bash
