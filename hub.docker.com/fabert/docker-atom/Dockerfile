FROM ubuntu:xenial

ENV TERM=xterm
ENV ATOM_PACKAGES="file-icons remote-sync terminal-plus atom-autocomplete-php docblockr linter linter-php php-fmt"

RUN apt-get -qq update && \
    apt-get -qq install \
        ca-certificates \
        composer \
        curl \
        fakeroot \
        gconf-service \
        gconf2 \
        git \
        gvfs-bin \
        libasound2 \
        libcap2 \
        libgconf-2-4 \
        libgtk2.0-0 \
        libnotify4 \
        libnss3 \
        libx11-xcb1 \
        libxkbfile1 \
        libxss1 \
        libxtst6 \
        php7.0-cli \
        python \
        xdg-utils \
        -qq -y --allow-unauthenticated --no-install-recommends && \
    rm -rf /var/lib/apt/lists/* && \
    curl -L https://atom.io/download/deb > /tmp/atom.deb && \
    dpkg -i /tmp/atom.deb && \
    rm -f /tmp/atom.deb && \
    apm install ${ATOM_PACKAGES} && \
    apm rebuild ${ATOM_PACKAGES} && \
    curl -L https://github.com/phpfmt/releases/raw/master/releases/lts/803.3/fmt.phar > /root/fmt.phar

COPY config.cson /root/.atom/config.cson

VOLUME /workspace

CMD ["/usr/bin/atom","-f", "/workspace"]
