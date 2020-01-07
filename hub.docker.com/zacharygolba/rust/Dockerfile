FROM fedora:28

ARG TOOLCHAIN=stable

COPY login.sh /tmp/login.sh

RUN set -e; \
    dnf upgrade -y; \
    dnf install gcc -y; \
    dnf clean all; \
    useradd -m rust; \
    cat /tmp/login.sh >> /home/rust/.bash_profile; \
    rm -rf /tmp/*

USER rust
ENV PATH=/home/rust/.cargo/bin:$PATH
WORKDIR /home/rust

RUN set -eu; \
    curl https://sh.rustup.rs -sSf | sh -s -- \
        --default-toolchain ${TOOLCHAIN} \
        --no-modify-path \
        -y; \
    cargo install ferris-says

ENTRYPOINT [ "/bin/bash", "--login", "-c" ]
CMD [ "/bin/bash" ]
