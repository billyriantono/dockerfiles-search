FROM ocaml/opam
RUN  opam install -y oUnit 
RUN  opam install -y utop
COPY sources.list /etc/apt
RUN sudo apt update
RUN sudo apt install python -y
RUN sudo apt install cmake -y
RUN opam install ppx_deriving -y
RUN opam depext conf-llvm.3.9 -y
RUN opam install "llvm=3.9" -y
