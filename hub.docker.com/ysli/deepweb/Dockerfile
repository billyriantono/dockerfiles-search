FROM ysli/vst:2.3
ENV OPAMYES true
RUN opam repo add coq-extra-dev https://coq.inria.fr/opam/extra-dev \
 && opam update \
 && opam pin coq-itree 1.0.0 \
 && opam install coq-ceres \
 && opam install coq-quickchick \
 && opam install coq-reduction-effects \
 && opam install coq-metalib \
 && sudo apt-get update \
 && sudo apt-get install -y procps git haskell-stack netbase cmake \
 && git clone https://github.com/plclub/lngen.git \
 && cd lngen \
 && stack setup \
 && stack install \
 && echo "PATH+=:$(stack path --local-bin)" >> ~/.profile
