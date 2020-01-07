FROM debian:jessie
WORKDIR /root
RUN apt-get update
RUN apt-get -f install
RUN apt-get install -y git build-essential ncurses-dev lua5.2 lua5.2-dev luajit python-dev python3-dev ruby-dev make autoconf automake gcc g++ vim tig dbus bash-completion supervisor bzip2 unzip p7zip-full tree sed silversearcher-ag pandoc locales dialog chrony openssl curl wget ftp ncftp subversion mutt msmtp expect cron dnsutils procps siege htop inetutils-traceroute iftop bmon iptraf nload slurm sl toilet lolcat lsb-release
RUN git clone https://github.com/vim/vim
WORKDIR /root/vim
RUN git checkout -b v8.0.0823
RUN ./configure --with-features=huge --enable-multibyte --enable-luainterp=dynamic --enable-gpm --enable-cscope --enable-fontset --enable-fail-if-missing --prefix=/usr/local --enable-pythoninterp=dynamic --enable-python3interp=dynamic --enable-rubyinterp=dynamic
RUN make && make install
