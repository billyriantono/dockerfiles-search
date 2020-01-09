FROM ubuntu:16.04
RUN apt-get update
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:bitcoin/bitcoin -y
RUN apt-get update
RUN apt-get install -y build-essential libssl1.0.0 libdb++-dev libboost-all-dev miniupnpc libqrencode-dev git libssl-dev libminiupnpc-dev libleveldb-dev 
RUN git clone https://github.com/Gr1dd/CompCoin.git
RUN /bin/sh -c 'cd /CompCoin/src/leveldb && make'
RUN /bin/sh -c 'cd /CompCoin/src && make -f makefile.unix  && chmod 777 leveldb/ -R'
RUN /bin/sh -c 'cd /CompCoin/src && export PASS=rpcpassword=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1)  && echo $PASS | tee --append test.conf'
RUN /bin/sh -c 'cd /CompCoin/src && chmod 700 test.conf'
CMD /bin/sh -c 'cd /CompCoin/src && ./CompCoind -conf=$PWD/test.conf -seednode=fleabags.net -addnode=fleabags.net -dns -debug -debugnet -dnsseed -upnp'
