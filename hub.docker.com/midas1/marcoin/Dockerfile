FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./marcoind .
COPY ./marcoin-cli .

RUN chmod +x ./* && \
    ln marcoind walletd && \
    ln marcoin-cli wallet-cli

VOLUME ["/root/.marcoin"]
EXPOSE 44004

RUN walletd --help || exit $(($? == 127))
