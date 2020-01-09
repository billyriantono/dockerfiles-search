FROM mikeifomin/midas_wallet_base:v1-zeromq-dev

RUN apt-get update && \
    apt-get --no-install-recommends --yes install \
    libdb5.3++-dev

WORKDIR /usr/local/bin

COPY ./stipendd .
COPY ./stipend-cli .

RUN chmod +x ./* && \
    ln stipendd walletd && \
    ln stipend-cli wallet-cli 

VOLUME ["/root/.stipend"]
EXPOSE 46978

RUN walletd --help || exit $(($? == 127))
