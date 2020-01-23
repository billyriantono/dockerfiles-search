FROM ubuntu:18.04

# install base packages
RUN apt-get update -qq && \
 DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common build-essential libpq-dev libsqlite3-dev libmysqlclient-dev git autoconf locales locales-all curl wget vim openssl libssl-dev libyaml-dev libxslt1-dev libevent-dev cmake htop libreadline7 libreadline-dev libtool automake bzip2 ca-certificates libffi-dev procps zlib1g-dev xz-utils libxml2-dev libncurses5-dev libglib2.0-dev libbz2-dev tzdata libsodium-dev && \
 curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
 curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
 echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
 apt-get update -qq && \
 apt-get install -y nodejs yarn && \
 apt-get clean && \
 rm -rf /var/lib/apt/lists/*

RUN mkdir /secp256k1
WORKDIR /secp256k1
RUN git clone https://github.com/bitcoin-core/secp256k1.git . && ./autogen.sh && ./configure --enable-module-recovery && make && make install
WORKDIR /

# set language
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV LC_ALL en_US.UTF-8

CMD [ "bash" ]
