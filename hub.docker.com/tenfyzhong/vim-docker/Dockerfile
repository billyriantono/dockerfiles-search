FROM alpine:3.4
MAINTAINER tenfyzhong "tenfyzhong@qq.com"

ENV VIM_VERSION 7.4.774

RUN apk update \
        && apk add --no-cache \
        git \
        gcc \
        libc-dev \
        make \
        gettext \
        ncurses-dev \
        acl-dev \
        libxmu-dev \
        gtk+2.0-dev \
        libxpm-dev \
        perl-dev \
        python-dev \
        python3-dev \
        ruby \
        ruby-dev \
        lua5.3-dev \
        luajit-dev \
        ca-certificates \
        wget \
        && update-ca-certificates \
        && wget https://codeload.github.com/vim/vim/tar.gz/v7.4.774 \
        && tar xzf v${VIM_VERSION} \
        && cd vim-${VIM_VERSION} \
        && ./configure --prefix=/opt/vim --enable-fail-if-missing --with-features=huge --enable-pythoninterp --enable-python3interp --enable-rubyinterp --enable-luainterp --with-luajit \
        && make \
        && make install \
        && cd .. \
        && rm -rf vim-${VIM_VERSION} \
        && apk del --purge git gcc libc-dev make gettext ncurses-dev libxmu-dev ruby

WORKDIR /root

ENTRYPOINT ["/opt/vim/bin/vim"]
CMD [""]
