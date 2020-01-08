FROM mikeifomin/midas_wallet_base:v1-zeromq-dev

WORKDIR /usr/local/bin

COPY ./wavercoind .
COPY ./wavercoin-cli .

RUN chmod +x ./* && \
    ln wavercoind walletd && \
    ln wavercoin-cli wallet-cli

VOLUME ["/root/.wavercoin"]
EXPOSE 21501

RUN walletd --help || exit $(($? == 127))
