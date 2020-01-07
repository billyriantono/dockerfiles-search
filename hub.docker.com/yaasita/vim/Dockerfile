FROM debian:stretch
MAINTAINER yaasita

#apt
ADD sources.list /etc/apt/sources.list
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y wget
RUN apt-get build-dep -y vim

#vim
RUN cd /root \
    && wget https://github.com/vim/vim/archive/v8.0.0000.tar.gz \
    && tar xvaf v8.0.0000.tar.gz
RUN cd /root/vim-* \
    && ./configure --with-features=huge --enable-fail-if-missing --enable-perlinterp --enable-pythoninterp --enable-rubyinterp \
    && make install \
    && ln -s /usr/local/bin/vim /usr/local/bin/vi

