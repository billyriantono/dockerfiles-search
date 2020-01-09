FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./lrmcoind .
COPY ./lrmcoin-cli .

RUN chmod +x ./* && \
    ln lrmcoind walletd && \
    ln lrmcoin-cli wallet-cli

VOLUME ["/root/.lrmcoin"]
EXPOSE 17273

RUN walletd --help || exit $(($? == 127))
