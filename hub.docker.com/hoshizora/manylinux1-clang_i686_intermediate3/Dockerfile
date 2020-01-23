FROM hoshizora/manylinux1-clang_i686_intermediate2:clang3

LABEL maintainer='amaya <mail@sapphire.in.net>'

WORKDIR /root

RUN set -eux && \
    `# Build clang 3.9.1 (cont.)` \
    cd llvm-build && \
    (make -j2) & sleep 6000 ; ps $! > /dev/null 2>&1 && kill -9 $! || :

