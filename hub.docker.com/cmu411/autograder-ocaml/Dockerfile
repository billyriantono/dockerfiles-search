FROM cmu411/autograder:latest

ENV ocaml_version=4.08.0+flambda

RUN apt-get update && apt-get install -y \
    aspcud \
    bubblewrap \
    cmake \
    libcap2 \
    m4 \
    pkg-config \
    unzip \
  && \
  bash -c "sh <(curl -sL https://raw.githubusercontent.com/ocaml/opam/master/shell/install.sh) <<< ''" && \
  opam init --dot-profile=~/.bashrc \
    --comp="$ocaml_version" --auto-setup \
    --disable-sandboxing --reinit


# Package installation
RUN opam update -y && opam install -y \
  cmdliner \
  core \
  getopt \
  jbuilder \
  llvm.6.0.0 \
  menhir \
  ocamlfind \
  ocamlgraph \
  ounit \
  ppx_jane \
  ppx_let \
  ;

#--------------
# MISC PACKAGE INSTALLATION -- common to all Dockerfiles
# Add convenience packages for students using container.
#--------------
RUN apt-get update && apt-get install -y \
  emacs \
  gdb \
  python3 \
  vim \
  ;
