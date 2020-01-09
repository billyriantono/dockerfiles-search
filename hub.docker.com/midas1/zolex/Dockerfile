FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./zolexcoind .
COPY ./zolexcoin-cli .

RUN chmod +x ./* && \
    ln zolexcoind walletd && \
    ln zolexcoin-cli wallet-cli

VOLUME ["/root/.zolexcoin"]
EXPOSE 33342

RUN walletd --help || exit $(($? == 127))
