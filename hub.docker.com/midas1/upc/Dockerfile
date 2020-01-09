FROM mikeifomin/midas_wallet_base:v1-zeromq-dev

WORKDIR /usr/local/bin

COPY ./ultrapaycoind .
COPY ./ultrapaycoin-cli .

RUN chmod +x ./* && \
    ln ultrapaycoind walletd && \
    ln ultrapaycoin-cli wallet-cli

VOLUME ["/root/.ultrapaycoin"]
EXPOSE 13333

RUN walletd --help || exit $(($? == 127))
