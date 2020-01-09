FROM debian:bullseye-slim

RUN apt-get update -qq \
  && apt-get install -qq --no-install-recommends \
    curl \
    gnupg2 \
    ca-certificates \
    git \
    ssh \
    tar \
    gzip \
    m4 \
    opam \
    ocaml

RUN useradd -m -s /bin/bash ocaml
USER ocaml
WORKDIR /home/ocaml

RUN opam init --yes --disable-sandbox --compiler=ocaml-system.4.08.1
RUN eval $(opam env) \
  && opam update --yes \
  && opam install --yes \
    dune \
    base \
    core_kernel \
    ppx_compare \
    ppx_custom_printf \
    ppx_hash \
    ppx_sexp_conv \
    ppxlib \
    stdio

CMD ["/bin/bash"]
