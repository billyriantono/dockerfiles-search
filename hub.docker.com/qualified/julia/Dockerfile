FROM julia:1.0.3-stretch

RUN useradd --create-home codewarrior
RUN set -ex; \
    mkdir /workspace; \
    chown codewarrior:codewarrior /workspace;

WORKDIR /workspace

USER codewarrior
ENV USER=codewarrior \
    HOME=/home/codewarrior
RUN set -ex; \
    julia -e "import Pkg; Pkg.add(Pkg.PackageSpec(url=\"https://github.com/kazk/FactCheck.jl\", rev=\"0324914232099edf655d808bc8bf95e4d673dde5\"))"; \
    julia -e "import FactCheck;"; \
    rm -rf ~/.julia/registries;
