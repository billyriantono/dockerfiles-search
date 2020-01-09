FROM ubuntu:rolling AS build

ARG repository=https://github.com/eXperiencePoints/XPCoin.git
ARG branch=1.1.0

WORKDIR /tmp
RUN apt-get update -qq
RUN apt-get install -qq -y --no-install-recommends ca-certificates git build-essential libboost-all-dev libssl-dev libdb-dev libdb++-dev
RUN git clone -b ${branch} ${repository} .
ADD *.patch ./
RUN patch -p1 -i fix-create-conf.patch
RUN patch -p1 -i fix-seed-addresses.patch
RUN patch -p1 -i fix-testnet.patch
RUN patch -p1 -i mod-checkpoints.patch
RUN patch -p1 -i mod-disconnect-olders.patch

WORKDIR /tmp/src
RUN make -f makefile.unix STATIC=1 USE_O3=1 USE_LEVELDB=1 USE_ASM=1
RUN strip XPd


FROM ubuntu:zesty AS publish
COPY --from=build /tmp/src/XPd /usr/local/bin
RUN ln -s /srv /root/.XP

EXPOSE 28192 28191
VOLUME ["/srv"]
ENTRYPOINT ["/usr/local/bin/XPd", "-printtoconsole", "-pid=/run/XPd.pid", "-datadir=/srv"]
CMD ["-server=0"]
