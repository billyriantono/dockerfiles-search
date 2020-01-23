FROM debian:stable-slim

LABEL maintainer="Sorav Bansal <sorav@compiler.ai>"

COPY apt.conf /etc/apt/apt.conf

ARG proxy

RUN /bin/true \
  && export http_proxy=$proxy \
  && export https_proxy=$proxy \
  && export ftp_proxy=$proxy \
  && DEBIAN_FRONTEND=noninteractive apt-get update \
  && apt-get dist-upgrade -y \
  && apt-get install -y \
      g++-8 \
      wget \
      ca-certificates \
      make \
      rsync \
      sudo \
      git \
      cmake libboost-all-dev flex bison unzip \
      gperf libgmp3-dev autoconf \
      libiberty-dev libc6-dev-i386 g++-multilib binutils-dev bison flex ocaml camlidl zlib1g-dev glib-2.0 expect rpcbind libswitch-perl gperf libgmp-dev libboost-dev libboost-iostreams-dev coq llvm llvm-dev camlp5 libelf-dev clang-6.0 clang++-6.0 ocaml-findlib ninja-build z3 libz3-dev libmagic-dev python python-pip \
      ruby ruby-dev gem freetds-dev \
      menhir ocaml-libs \
      nodejs \
      npm \
  && apt-get autoremove --purge -y \
  && apt-get autoclean -y \
  && pip install python-magic \
  && gem install tiny_tds \
  && wget -r http://www.cse.iitd.ac.in/~sbansal/superopt-tars --accept-regex="http://www.cse.iitd.ac.in/~sbansal/superopt-tars" --no-verbose \
  && mv www.cse.iitd.ac.in/~sbansal/superopt-tars /tars \
  && rm -rf www.cse.iitd.ac.in \
  && rm -rf /var/cache/apt/* /tmp/* \
  && ln -s /usr/bin/clang-6.0 /usr/bin/clang \
  && ln -s /usr/bin/clang++-6.0 /usr/bin/clang++ \
  && /bin/true

WORKDIR /

CMD ["bash"]
