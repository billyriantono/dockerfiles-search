FROM rakudo-star:2018.10

RUN set -ex; \
    useradd --create-home codewarrior; \
    ln -s /home/codewarrior /workspace;

WORKDIR /workspace

USER codewarrior
ENV USER=codewarrior \
    HOME=/home/codewarrior
