FROM debian:stretch

ENV hash=
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get install -qq git build-essential gnat flex bison libncurses5-dev wget zlib1g-dev vim gcc-multilib
RUN cd /root/ ; \
    git clone https://review.coreboot.org/coreboot ; \
    cd coreboot ; \
    git submodule update --init --checkout

COPY entrypoint.sh /usr/local/bin
RUN chmod +x /usr/local/bin/entrypoint.sh
RUN ln -s usr/local/bin/entrypoint.sh / # backwards compat

ENTRYPOINT ["entrypoint.sh"]

CMD ["bash"]
