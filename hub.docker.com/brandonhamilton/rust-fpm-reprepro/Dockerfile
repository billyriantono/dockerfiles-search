FROM rust:latest

RUN apt -qq update \
 && apt -qq upgrade -y \
 && apt -qq install -y ocaml libelf-dev ruby-dev rubygems build-essential clang pinentry-curses libarchive13 libgpgme11 gnupg2 libassuan0 gnupg-agent libksba8 libpth20 librocksdb-dev libasound2-dev \
 && wget -O /tmp/reprepo_amd64.deb http://ftp.debian.org/debian/pool/main/r/reprepro/reprepro_5.1.1-1_amd64.deb \
 && dpkg -i /tmp/reprepo_amd64.deb \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 && gem install fpm \
 && rustup component add rustfmt-preview
