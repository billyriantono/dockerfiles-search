FROM ubuntu:xenial as build
LABEL maintainer="https://github.com/senagbe"

# Build htmlcoin

RUN apt-get -y update
RUN apt-get -y install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils git cmake libboost-all-dev
RUN apt-get -y install software-properties-common
RUN add-apt-repository ppa:bitcoin/bitcoin
RUN apt-get -y update
RUN apt-get -y install libdb4.8-dev libdb4.8++-dev

# enable zeromq
RUN apt-get -y install libzmq3-dev

RUN apt-get -y install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler

RUN git clone -b "v2.0.0.3" https://github.com/HTMLCOIN/HTMLCOIN --recursive
WORKDIR HTMLCOIN

# Note autogen will prompt to install some more dependencies if needed
RUN ./autogen.sh
RUN ./configure
RUN make -j2

COPY --from=build /HTMLCOIN/src/htmlcoind /bin/htmlcoind
COPY --from=build /HTMLCOIN/src/htmlcoin-tx /bin/htmlcoin-tx
COPY --from=build /HTMLCOIN/src/htmlcoin-cli /bin/htmlcoin-cli

LABEL version="2.0.0.3"

EXPOSE 4889
EXPOSE 14889

ENTRYPOINT ["/bin/htmlcoind"]
CMD ["-help"]
