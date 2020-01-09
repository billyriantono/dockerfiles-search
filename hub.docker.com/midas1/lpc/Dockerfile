FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./lightpaycoind .
COPY ./lightpaycoin-cli .

RUN chmod +x ./* && \
    ln lightpaycoind walletd && \
    ln lightpaycoin-cli wallet-cli

VOLUME ["/root/.lightpaycoin"]
EXPOSE 39797

RUN walletd --help || exit $(($? == 127))
