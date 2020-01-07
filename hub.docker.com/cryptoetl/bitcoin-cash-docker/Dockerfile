FROM ubuntu
LABEL maintainer="Allen Day allenday@allenday.com"
RUN apt-get update && apt-get install -y software-properties-common build-essential wget pkg-config
RUN apt-get install -y libboost-all-dev libssl-dev libevent-dev
RUN apt-get install -y bsdmainutils
WORKDIR /opt
RUN wget https://download.bitcoinabc.org/0.18.1/linux/bitcoin-abc-0.18.1.tar.gz
RUN tar -xvzf bitcoin-abc-0.18.1.tar.gz
WORKDIR /opt/bitcoin-abc-0.18.1
RUN ./configure --disable-wallet
RUN make -j4
