FROM ubuntu:16.04
WORKDIR /root

RUN apt-get update && apt-get install -y \
  ocaml \
  libgcrypt20-dev \
  ocaml-findlib \
  opam \
  m4 \
  git \
  vim \
  build-essential

RUN opam init -y && \
    opam switch -y 4.06.0 && \
    eval `opam config env` && \
    opam install -y camlp4 ocamlfind ocamlbuild batteries && \
    git clone https://github.com/samee/obliv-c.git && \
    cd obliv-c && \
    ./configure && make
