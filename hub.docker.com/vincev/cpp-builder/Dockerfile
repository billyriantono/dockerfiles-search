FROM fedora

RUN dnf -y update && \
    dnf -y install clang cmake gcc git make && \
    dnf clean all

ARG user=build

RUN useradd  -m -s /bin/bash ${user}

USER ${user}
WORKDIR /home/${user}
