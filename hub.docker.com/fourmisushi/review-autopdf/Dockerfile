FROM archlinux/base

RUN pacman -Syu --noconfirm \
                texlive-core \
                texlive-latexextra \
                texlive-langjapanese \
                zip \
                ruby \
		awk \
                inotify-tools

RUN gem install review rake && \
    mkdir /workdir
WORKDIR /workdir

COPY entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
